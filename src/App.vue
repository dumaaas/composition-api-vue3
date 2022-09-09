<template>
  <h1>Composition API | Vue 3</h1>
  <QuestionComponent />
</template>

<script setup>
import { provide, ref } from 'vue'

import QuestionComponent from "./components/QuestionComponent.vue";
const weekend = ref('Happy weekend');
provide('weekend', weekend);

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
    margin-bottom: 60px;
}
</style>
