<script setup>
import { data } from './server/data';

const $toast = useToast();

const normasLaudoTecnico = ref([]);

const fetchData = async () => {
  normasLaudoTecnico.value = data;
}

const searchInput = ref('');
const filteredNormasLaudoTecnico = ref([...normasLaudoTecnico.value]);

const filterOptions = computed(() => {
  searchInput.value = searchInput.value.toString();
  if (searchInput.value === '') {
    filteredNormasLaudoTecnico.value = normasLaudoTecnico.value;
    return;
  }

  filteredNormasLaudoTecnico.value = normasLaudoTecnico.value.filter((norma) =>
    norma.title.includes(searchInput.value.toUpperCase())
  );
});

async function copyCardImageToClipboard(item, key) {
  const imgElement = document.getElementById(`${item.title.replaceAll(' ', '-')}-${key}`);
  try {
    const canvas = document.createElement("canvas");
    const context = canvas.getContext("2d");

    canvas.width = imgElement.width;
    canvas.height = imgElement.height;

    context.drawImage(imgElement, 0, 0);

    const blob = await new Promise((resolve) => canvas.toBlob(resolve, "image/png"));

    const clipboardItem = new ClipboardItem({ "text/plain": new Blob([item.description], { type: 'text/plain' }), "image/png": blob });

    console.dir(clipboardItem);
    await navigator.clipboard.write([clipboardItem]);

    console.log("Image copied to clipboard!");
  } catch (error) {
    console.error("Failed to copy image:", error);
  }
}

const cards = ref([]);
const cardRefs = ref([]);
const setEqualHeight = () => {
  const maxHeight = Math.max(...cardRefs.value.map(card => card.offsetHeight));
  cardRefs.value.forEach((card) => {
    card.style.height = `${maxHeight}px`;
  });
};

onMounted(() => {
  fetchData();
  cardRefs.value = Array.from(document.querySelectorAll('.card-content'));
  setEqualHeight();
});
watch(searchInput, () => {
  cardRefs.value = Array.from(document.querySelectorAll('.card-content'));
  setEqualHeight();
});

const selectedItem = ref({});
const isOpen = ref(false);
const onDialogOpen = (item) => {
  isOpen.value = true;
  console.log(item);
  selectedItem.value = item;
};

</script>

<template>
  <div class="bg-slate-900 h-screen w-screen">
    <div class="w-screen px-40 py-10 flex flex-col justify-center items-center">
      <UInput v-model="searchInput" type="text" color="blue" outlined class="w-96" placeholder="Pesquisar" size="lg"
        icon="i-heroicons-magnifying-glass" @change="filterOptions" />
      <UContainer
        class="bg-slate-900 rounded-md mt-6 p-6 gap-5 overflow-y-auto overflow-x-hidden pt-7 flex flex-wrap justify-center lg:justify-between items-center transition-all w-full max-h-[86svh] h-fit">
        <UCard v-if="!!filteredNormasLaudoTecnico.length" v-for="(item, key) in filteredNormasLaudoTecnico" :key="key"
          :ref="cardRefs" class="w-full md:w-96 sm:w-96 h-auto divide-none">
          <template #header>
            {{ item.title }}
          </template>
          <div class="card-content">
            <div class="mb-4">{{ item.resume }}</div>
            <img v-if="item.imgUrl" class="mb-4 rounded-md" :id="`${item.title.replaceAll(' ', '-')}-${key}`"
              :src="item.imgUrl">
          </div>



          <template #footer class="max-h-1">
            <UContainer class="flex flex-row justify-center items-center content-center gap-4">
              <UButton size="lg" variant="soft" color="blue" icon="i-heroicons-clipboard" label="Copiar"
                class="transition-all ease-in-out" @click="copyCardImageToClipboard(item, key)" />
              <UButton size="lg" variant="soft" color="yellow" icon="i-heroicons-eye" label="Visualizar"
                class="transition-all ease-in-out" @click="onDialogOpen(item)" />
            </UContainer>
          </template>
        </UCard>
        <Ucard v-else
          class="bg-slate-800 w-full text-center flex align-middle justify-center items-center rounded-lg h-10">
          <span>Nenhuma norma encontrada</span>
        </Ucard>
      </UContainer>
    </div>

    <UModal v-model="isOpen">
      <UCard class="w-full h-auto divide-none">
        <template #header>
          {{ selectedItem.title }}
        </template>
        <div class="card-content flex flex-col text-left justify-center">
          <div class="mb-4">{{ selectedItem.description }}</div>
          <img class="mb-4" :src="selectedItem.imgUrl">
        </div>
        <template #footer>
          <UContainer class="flex flex-row justify-center items-center content-center gap-4">
            <UButton size="lg" icon="i-heroicons-clipboard" variant="soft" label="Copiar" color="blue"
              class="transition-all ease-in-out" @click="copyCardImageToClipboard(item, key)" />
            <UButton size="lg" icon="i-heroicons-x-mark" variant="ghost" label="Fechar" color="red"
              class="transition-all ease-in-out" @click="isOpen = false" />
          </UContainer>
        </template>
      </UCard>
    </UModal>
  </div>
</template>
