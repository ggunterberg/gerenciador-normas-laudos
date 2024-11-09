<script setup>
const $toast = useToast();

const normasLaudoTecnico = [
  {
    title: 'ABNT NBR 14724',
    resume: 'Norma para a apresentação de trabalhos acadêmicos.',
    description: 'A NBR 14724 estabelece os requisitos para formatação e apresentação de trabalhos acadêmicos, como monografias, dissertações e teses, orientando sobre aspectos como capa, sumário, referências, entre outros.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  },
  {
    title: 'ABNT NBR 5413',
    resume: 'Iluminância de ambientes internos.',
    description: 'A norma NBR 5413 define os valores de iluminância recomendados para diferentes tipos de ambientes internos, como escritórios e escolas, visando ao conforto visual e à eficiência no consumo de energia.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  },
  {
    title: 'ABNT NBR 10152',
    resume: 'Níveis de ruído em ambientes internos.',
    description: 'A NBR 10152 estabelece os níveis de ruído recomendados para diferentes ambientes, como salas de aula e escritórios, visando o conforto acústico e a saúde dos usuários.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  },
  {
    title: 'ABNT NBR 9050',
    resume: 'Acessibilidade a edificações, mobiliário, espaços e equipamentos urbanos.',
    description: 'Esta norma fornece diretrizes para promover a acessibilidade em edificações e espaços urbanos, garantindo a inclusão de pessoas com deficiência ou mobilidade reduzida.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  },
  {
    title: 'ABNT NBR 5410',
    resume: 'Instalações elétricas de baixa tensão.',
    description: 'A norma NBR 5410 trata das condições técnicas exigidas para garantir a segurança em instalações elétricas de baixa tensão, desde a concepção até a execução.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  },
  {
    title: 'ABNT NBR 6023',
    resume: 'Referências bibliográficas.',
    description: 'A norma NBR 6023 estabelece regras para elaboração de referências bibliográficas, padronizando a apresentação de informações de fontes utilizadas em trabalhos técnicos e acadêmicos.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  },
  {
    title: 'ABNT NBR 10520',
    resume: 'Citações em documentos.',
    description: 'A norma NBR 10520 orienta sobre a forma correta de fazer citações de autores em documentos acadêmicos, detalhando o uso de citações diretas e indiretas.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  },
  {
    title: 'ABNT NBR ISO 9001',
    resume: 'Sistema de gestão da qualidade.',
    description: 'A norma ISO 9001 define os requisitos para um sistema de gestão da qualidade, focando na melhoria contínua dos processos e na satisfação do cliente.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  },
  {
    title: 'ABNT NBR ISO 14001',
    resume: 'Sistema de gestão ambiental.',
    description: 'A ISO 14001 é uma norma internacional que fornece diretrizes para a implementação de um sistema de gestão ambiental, visando a redução de impactos ao meio ambiente.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  },
  {
    title: 'ABNT NBR 5991',
    resume: 'Instalações de equipamentos médicos.',
    description: 'A norma NBR 5991 apresenta requisitos para a instalação segura de equipamentos médicos em unidades de saúde, visando a segurança dos pacientes e dos profissionais de saúde.',
    imgUrl: 'https://media.istockphoto.com/id/472290125/pt/vetorial/gato-em-windowsill.jpg?s=612x612&w=0&k=20&c=B0_F90grQj7RCjNoFhqX8YEVoRu9bMKaBRXX5One82o='
  }
];

const searchInput = ref('');
const filteredNormasLaudoTecnico = ref([...normasLaudoTecnico]);

const filterOptions = computed(() => {
  searchInput.value = searchInput.value.toString();
  if (searchInput.value === '') {
    filteredNormasLaudoTecnico.value = normasLaudoTecnico;
    return;
  }

  filteredNormasLaudoTecnico.value = normasLaudoTecnico.filter((norma) =>
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
        <UCard v-for="(item, key) in filteredNormasLaudoTecnico" :key="key" :ref="cardRefs"
          class="w-full md:w-96 sm:w-96 h-auto divide-none">
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

<style>
/* .container-box {
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(10px);

  scrollbar-width: thin;
} */
</style>
