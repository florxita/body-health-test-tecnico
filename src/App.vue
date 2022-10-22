<script setup>
import { ref, onMounted, computed, watch } from "vue";
import Card from "./components/Card.vue";

const noticias = ref([]);
const loading = ref(true);

const getData = async () => {
  try {
    const response = await fetch("http://127.0.0.1:5173/src/api/data.json");
    noticias.value = await response.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  }

  console.log(noticias);
};

onMounted(() => {
  getData();
});
</script>

<template>
  <h1>Stetic News</h1>
  <p v-if="loading">Cargando</p>
  <div v-if="!loading" class="container">
    <Card
      v-for="noticia in noticias"
      :category="noticia.category"
      :region="noticia.region"
      :body="noticia.body"
      :url="noticia.url"
    />
  </div>
</template>

<style></style>
