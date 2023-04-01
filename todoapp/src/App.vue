<template>
  <h1>動的コンポーネント</h1>
  <select @change="switchComp">コンポーネントを切り替える
    <option value="Input">Input</option>
    <option value="Radio">Radio</option>
    <option value="Select">Select</option>
  </select>
  <p>コンポーネント名： {{ currentCompName }}</p>
  
  <keep-alive>
    <component :is="currentComp" />
  </keep-alive>
</template>


<script setup lang="ts">
import { ref } from "vue";
import BaseInput from "./components/BaseInput.vue";
import BaseRadio from "./components/BaseRadio.vue";
import BaseSelect from "./components/BaseSelect.vue";

const currentComp = ref(BaseInput);
const currentCompName = ref("Input");
// .vueファイルを読み込んだコンポーネントオブジェクトのデータ型は複雑なので，型の指定は行わない．
const compList = [BaseInput, BaseRadio, BaseSelect];
const compNameList: string[] = ["Input", "Radio", "Select"];

let currentCompIdx = 0;
const switchComp = () => {
  currentCompIdx = ++currentCompIdx % compList.length;
  currentComp.value = compList[currentCompIdx];
  currentCompName.value = compNameList[currentCompIdx];

}
</script>


<style scoped>
.dynamic-component {
  border: green 1px solid;
}
</style>
