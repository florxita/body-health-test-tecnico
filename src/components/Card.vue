<script setup>
import { ref, computed } from "vue";

const { body, url } = defineProps({
  id: Number,
  category: String,
  region: String,
  body: String,
  hour: String,
  url: Array,
});

const bodySliced = ref("");
const links = ref("");

bodySliced.value = body.slice(0, 254).concat("..."); //reduzco cantidad de caracteres a 255 y concateno con "..."

const fillLinks = () => {
  links.value = url.map((link) => {
    const cuttedLink = link.split("/")[2];

    if (cuttedLink.includes("www")) {
      return {
        originalLink: link,
        linkWithoutW: cuttedLink.slice(4),
      };
    }
    return {
      originalLink: link,
      linkWithoutW: cuttedLink,
    };
  });
};

fillLinks();
</script>

<template>
  <div class="card">
    <div class="flex">
      <h2>{{ category }}</h2>
      <h2>{{ region }}</h2>
    </div>
    <article>
      <p>
        {{ bodySliced }}
      </p>
    </article>
    <div class="flex">
      <span>{{ hour }}</span>
      <span v-for="link in links" :key="link">
        <a :href="link.originalLink" target="_blank">
          ver en {{ link.linkWithoutW }}</a
        >
        <!-- 
          ** Intento concatenar los 2 links para que queden conectados por un "y en" pero no funciona correctamente
          <a :href="link.originalLink" target="_blank"
          >{{ links.length > 1 && "y en" }} {{ link.linkWithoutW }}</a
        > -->
      </span>
    </div>
  </div>
</template>

<style>
.flex {
  display: flex;
  justify-content: space-between;
}
.card {
  width: 600px;
  font-family: sans-serif;
  display: flex;
  flex-direction: column;
  padding: 2rem;
  border-radius: 25px;
  background-color: aliceblue;
}
</style>
