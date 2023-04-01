<template>
    <div class="dynamic-component">
        <input type="text" v-model="inputValue">
        <p>{{ inputValue }}</p>
    </div>
</template>


<script setup lang="ts">
import { ref } from "vue";
const inputValue = ref("Hello Vue!");

</script>


<style scoped></style>