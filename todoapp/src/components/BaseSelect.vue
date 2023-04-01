<template>
    <div class="dynamic-component">
        <select v-model="memberType">
            <option value="1">通常会員</option>
            <option value="2">有料会員</option>
            <option value="3">非会員</option>
        </select>
        <br>
        <p>選択されたリスト: {{ memberType }}</p>
    </div>
</template>


<script setup lang="ts">
import { ref } from "vue";

const memberType = ref(1);
</script>


<style scoped></style>