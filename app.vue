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

    const clipboardItem = new ClipboardItem({
      "text/plain": new Blob([item.description], { type: 'text/plain' }),
      "image/png": blob 
    });

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
  <div class="bg-slate-900">
    <UContainer class="h-[10vh] p-5">
      <UInput v-model="searchInput" type="text" color="blue" outlined class="w-full" placeholder="Pesquisar"
        icon="i-heroicons-magnifying-glass" @change="filterOptions" />
    </UContainer>

    <UContainer class="h-[90vh] overflow-y-auto flex flex-wrap gap-5 py-16 px-10">

      <UCard v-if="!!filteredNormasLaudoTecnico.length" v-for="(item, key) in filteredNormasLaudoTecnico" :key="key"
        :ref="cardRefs" class="max-w-96 grow divide-none">

        <template #header>
          {{ item.title }}
        </template>

        <div class="h-[160px] overflow-y-hidden text-ellipsis">{{ item.description }}</div>

        <template #footer class="max-h-1">
          <UContainer class="flex justify-center gap-4">

            <UButton variant="soft" color="blue" icon="i-heroicons-clipboard" label="Copiar"
              class="transition-all ease-in-out" @click="copyCardImageToClipboard(item, key)" />

            <UButton variant="soft" color="yellow" icon="i-heroicons-eye" label="Visualizar"
              class="transition-all ease-in-out" @click="onDialogOpen(item)" />

          </UContainer>
        </template>

      </UCard>
      <Ucard v-else
        class="bg-slate-800 w-full text-center flex align-middle justify-center items-center rounded-lg h-10">
        <span>Nenhuma norma encontrada</span>
      </Ucard>
    </UContainer>

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
