<script setup>
const $toast = useToast();

const normasLaudoTecnico = [
  {
    title: 'ABNT NBR 14724',
    resume: 'Norma para a apresentação de trabalhos acadêmicos.',
    description: 'A NBR 14724 estabelece os requisitos para formatação e apresentação de trabalhos acadêmicos, como monografias, dissertações e teses, orientando sobre aspectos como capa, sumário, referências, entre outros.',
    imgUrl: 'data:image/jpeg;base64,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'
  },
  {
    title: 'ABNT NBR 5413',
    resume: 'Iluminância de ambientes internos.',
    description: 'A norma NBR 5413 define os valores de iluminância recomendados para diferentes tipos de ambientes internos, como escritórios e escolas, visando ao conforto visual e à eficiência no consumo de energia.',
    imgUrl: 'https://example.com/img/nbr5413.jpg'
  },
  {
    title: 'ABNT NBR 10152',
    resume: 'Níveis de ruído em ambientes internos.',
    description: 'A NBR 10152 estabelece os níveis de ruído recomendados para diferentes ambientes, como salas de aula e escritórios, visando o conforto acústico e a saúde dos usuários.',
    imgUrl: 'https://example.com/img/nbr10152.jpg'
  },
  {
    title: 'ABNT NBR 9050',
    resume: 'Acessibilidade a edificações, mobiliário, espaços e equipamentos urbanos.',
    description: 'Esta norma fornece diretrizes para promover a acessibilidade em edificações e espaços urbanos, garantindo a inclusão de pessoas com deficiência ou mobilidade reduzida.',
    imgUrl: 'https://example.com/img/nbr9050.jpg'
  },
  {
    title: 'ABNT NBR 5410',
    resume: 'Instalações elétricas de baixa tensão.',
    description: 'A norma NBR 5410 trata das condições técnicas exigidas para garantir a segurança em instalações elétricas de baixa tensão, desde a concepção até a execução.',
    imgUrl: 'https://example.com/img/nbr5410.jpg'
  },
  {
    title: 'ABNT NBR 6023',
    resume: 'Referências bibliográficas.',
    description: 'A norma NBR 6023 estabelece regras para elaboração de referências bibliográficas, padronizando a apresentação de informações de fontes utilizadas em trabalhos técnicos e acadêmicos.',
    imgUrl: 'https://example.com/img/nbr6023.jpg'
  },
  {
    title: 'ABNT NBR 10520',
    resume: 'Citações em documentos.',
    description: 'A norma NBR 10520 orienta sobre a forma correta de fazer citações de autores em documentos acadêmicos, detalhando o uso de citações diretas e indiretas.',
    imgUrl: 'https://example.com/img/nbr10520.jpg'
  },
  {
    title: 'ABNT NBR ISO 9001',
    resume: 'Sistema de gestão da qualidade.',
    description: 'A norma ISO 9001 define os requisitos para um sistema de gestão da qualidade, focando na melhoria contínua dos processos e na satisfação do cliente.',
    imgUrl: 'https://example.com/img/iso9001.jpg'
  },
  {
    title: 'ABNT NBR ISO 14001',
    resume: 'Sistema de gestão ambiental.',
    description: 'A ISO 14001 é uma norma internacional que fornece diretrizes para a implementação de um sistema de gestão ambiental, visando a redução de impactos ao meio ambiente.',
    imgUrl: 'https://example.com/img/iso14001.jpg'
  },
  {
    title: 'ABNT NBR 5991',
    resume: 'Instalações de equipamentos médicos.',
    description: 'A norma NBR 5991 apresenta requisitos para a instalação segura de equipamentos médicos em unidades de saúde, visando a segurança dos pacientes e dos profissionais de saúde.',
    imgUrl: 'https://example.com/img/nbr5991.jpg'
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

function copyCardInfoToClipboard(item, key) {
  const textToCopy = `
  Titulo: ${item.title} \n
  Descrição: ${item.description} \n
  `;
  navigator.clipboard.writeText(textToCopy)
    .then(() => {
      console.log('copiado')
    })
    .catch(err => {
      console.error('Erro ao copiar texto: ', err);
    });
}

const cards = ref([]);
const cardRefs = ref([]);
const setEqualHeight = () => {
  const maxHeight = Math.max(...cardRefs.value.map(card => card.offsetHeight));

  cardRefs.value.forEach(card => {
    card.style.height = `${maxHeight}px`;
  });
};

onMounted(() => {
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
  <div class="bg-slate-900 h-screen">
    <div class="w-screen px-40 py-10">
      <UInput v-model="searchInput" type="text" variant="outline" placeholder="Pesquisar" size="lg"
        icon="i-heroicons-magnifying-glass" @change="filterOptions" />
      <UContainer
        class="container-box overlay rounded-md mt-6 p-6 gap-5 overflow-y-auto overflow-x-hidden pt-7 flex flex-wrap transition-all w-full max-h-[86svh] h-fit">
        <UCard v-for="(item, key) in filteredNormasLaudoTecnico" :key="key" :ref="cardRefs"
          class="w-full lg:w-96 h-auto">
          <template #header>
            {{ item.title }}
          </template>
          <div class="card-content">
            <div class="mb-4">{{ item.resume }}</div>
            <img class="mb-4" :id="`${item.title.replaceAll(' ', '-')}-${key}`" :src="item.imgUrl">
          </div>



          <template #footer>
            <UContainer class="flex flex-row justify-center items-center content-center gap-4">
              <UButton size="xs" label="Visualizar" @click="onDialogOpen(item)" />
              <UButton size="xs" icon="i-heroicons-document-duplicate" label="Imagem"
                @click="copyCardImageToClipboard(item, key)" />
              <UButton size="xs" icon="i-heroicons-document-duplicate" label="Informações"
                @click="copyCardInfoToClipboard(item, key)" />
            </UContainer>
          </template>
        </UCard>
      </UContainer>
    </div>

    <UModal v-model="isOpen">
      <div>
        <UCard class="w-full h-auto">
          <template #header>
            {{ selectedItem.title }}
          </template>
          <div class="card-content flex flex-col text-left justify-center">
            <div class="mb-4">{{ selectedItem.description }}</div>
            <img class="mb-4" :src="selectedItem.imgUrl">
          </div>
          <template #footer>
            <UContainer class="flex flex-row justify-center items-center content-center gap-4">
              <UButton size="lg" label="Copiar Imagem" @click="copyCardImageToClipboard(item, key)" />
              <UButton size="lg" label="Copiar Informações" @click="copyCardInfoToClipboard(item, key)" />
            </UContainer>
          </template>
        </UCard>
      </div>
    </UModal>
  </div>
</template>

<style>
.container-box {
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(10px);

  scrollbar-width: thin;
}
</style>
