<script setup>
import { ref, onMounted, computed, watch } from "vue";
import Card from "./components/Card.vue";
import Header from "./components/Header.vue";

const news = ref([]);
const loading = ref(true);

/**
 * Fetch Data Json
 */
const getData = async () => {
  try {
    const response = await fetch("http://127.0.0.1:5173/src/api/data.json");
    news.value = await response.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 1000);
  }
};

/** Funcion que se ejecuta cuando se carga el componente */
onMounted(() => {
  getData();
});
</script>

<template>
  <Header :news="news" />
  <p v-if="loading">Cargando</p>
  <div v-else="!loading" class="container">
    <Card
      v-for="_new in news"
      :key="_new.id"
      :category="_new.category"
      :region="_new.region"
      :body="_new.body"
      :hour="_new.hour"
      :url="_new.url"
    />
  </div>
</template>
