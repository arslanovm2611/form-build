<template>
  <div>
    <div class="grid grid-cols-8 gap-4">
      <formDetail v-for="p in pdf" :key="p" :pdf="p" />
    </div>
  </div>
</template>

<script setup>
const pdf = ref("");
async function fetchAndRenderPdf() {
  try {
    const response = await fetch(`http://localhost:3001/pdfs`);
    const jsonData = await response.json();
    pdf.value = jsonData;
  } catch (error) {
    console.error("Error fetching and rendering PDF:", error);
  }
}

onMounted(() => {
  fetchAndRenderPdf();
});
</script>
