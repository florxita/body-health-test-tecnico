<script setup>
import { ref } from "vue";

const { body } = defineProps({
  id: Number,
  category: String,
  region: String,
  body: String,
  hour: Date,
  url: Array,
});

const bodySliced = ref("");

/**
 * Funcion que limita cantidad de caracteres.
 */
bodySliced.value = body.slice(0, 254).concat("...");
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
      <span>{{ url }}</span>
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
