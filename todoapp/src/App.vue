<template>
  <h1>動的コンポーネント</h1>
  <button @click="switchComp">コンポーネントを切り替える</button>

  <p>コンポーネント名： {{ currentCompName }}</p>
  <KeepAlive>
    <component :is="currentComp" />
  </KeepAlive>
</template>


<script setup lang="ts">
import { ref } from "vue";
import BaseInput from "./components/BaseInput.vue";
import BaseRadio from "./components/BaseRadio.vue";
import BaseSelect from "./components/BaseSelect.vue";

const currentComp = ref(BaseInput);
const currentCompName = ref("Input");

const compList = [BaseInput, BaseRadio, BaseSelect];
const compNameList = ["Input", "Radio", "Select"];

let currentCompIdx = 0;
const switchComp = () => {
  currentCompIdx = ++currentCompIdx % compList.length;
  currentComp.value = compList[currentCompIdx];
  currentCompName.value = compNameList[currentCompIdx];

}
</script>


<style scoped></style>
