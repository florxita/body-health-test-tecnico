<script setup>
import { ref, computed } from "vue";

const { news } = defineProps({
  news: Object,
});

const search = ref(""); // input del user
// Estaba intentando filtrar la info de news traida como props desde el padre pero no funciona
// const filtroCategorias = news.value.filter((_new) => _new.category == "tendencias");

// console.log(filtroCategorias);
</script>
<template>
  <section class="header">
    <h1>Stetic News</h1>

    <input type="search" id="search" placeholder="Search" v-model="search" />
    <button @click="buscarEnCategoria">Buscar</button>
    <template v-for="_new in news" :key="_new.id">
      <!-- {{ _new.category }} -->
    </template>
  </section>
</template>
