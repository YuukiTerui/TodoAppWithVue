<template>
    <input type="text" v-model="inputValue">
    <p>{{ inputValue }}</p>
</template>


<script setup lang="ts">
import { ref } from "vue";
const inputValue = ref("Hello Vue!");

</script>


<style scoped>

</style>