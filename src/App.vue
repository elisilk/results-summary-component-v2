<script setup>
import ResultsSummary from './components/ResultsSummary.vue';
import data from './assets/data.json';
</script>

<template>
  <main>
    <h1 class="sr-only">Results Summary Component</h1>

    <ResultsSummary :data="data" />
  </main>
</template>

<style scoped></style>
