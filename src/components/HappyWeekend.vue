<script setup>
import { inject } from "vue";

const weekend = inject("weekend");
</script>

<template>
  <p>
    {{ weekend }}
  </p>
</template>

<style scoped>
    p {
        margin-top: 40px;
        padding-top: 20px;
        border-top: 1px solid #cacaca;
        color: #009688
    }
</style>
