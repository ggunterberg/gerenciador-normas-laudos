<script setup>
import { data } from './server/data';

const toast = useToast();

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

    if (imgElement) {
      canvas.width = imgElement.width;
      canvas.height = imgElement.height;
    }

    context.drawImage(imgElement, 0, 0);
    const imageBlob = await new Promise((resolve) => canvas.toBlob(resolve, "image/png"));
    const textBlob = new Blob([item.description], { type: 'text/plain' });
    const clipboardItem = new ClipboardItem({
      "text/plain": textBlob,
      "image/png": imageBlob ?? null,
    });

    console.dir(clipboardItem);
    await navigator.clipboard.write([clipboardItem]);

    console.log("Image copied to clipboard!");
    toast.add({
      title: `Copiado para o clipboard`,
      icon: 'i-heroicons-check-circle',
      description: 'Use CTRL+SHIFT+V para colar o texto',
      color: 'blue'
    });
  } catch (error) {
    console.error("Failed to copy image:", error);
  }
}

onMounted(() => {
  fetchData();
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
  <UContainer class="h-[10vh] p-5">
    <UInput v-model="searchInput" type="text" color="blue" outlined class="w-full" placeholder="Pesquisar"
      icon="i-heroicons-magnifying-glass" @change="filterOptions" />
  </UContainer>

  <UContainer class="h-[90vh] overflow-y-auto flex flex-wrap flex-row gap-5 py-10 content-start justify-left">

    <UCard v-if="!!filteredNormasLaudoTecnico.length" v-for="(item, key) in filteredNormasLaudoTecnico" :key="key"
      class="w-80 grow divide-none rounded-lg">

      <template #header>
        {{ item.title }}
      </template>

      <p class="overflow-hidden text-ellipsis line-clamp-3">
        {{ item.description }}
      </p>
      <div class="flex justify-center content-center p-10">
        <img src="public/defaultImage.jpg" width="300px" class="rounded-md" alt="image"
          :id="`${item.title.replaceAll(' ', '-')}-${key}`">
      </div>

      <template #footer>
        <UContainer class="flex justify-center gap-4">

          <UButton variant="soft" color="blue" icon="i-heroicons-clipboard" label="Copiar"
            class="transition-all ease-in-out" @click="copyCardImageToClipboard(item, key)" />

          <UButton variant="soft" color="yellow" icon="i-heroicons-eye" label="Visualizar"
            class="transition-all ease-in-out" @click="onDialogOpen(item)" />

        </UContainer>
      </template>

    </UCard>
    <Ucard v-else class="bg-slate-800 w-full text-center flex align-middle justify-center items-center rounded-lg h-10">
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
</template>