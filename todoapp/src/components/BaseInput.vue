<template>
    <input 
        :type="type"
        class="BaseInput"
        :class="classes"
        :disabled="disabled || loading"
        :placeholder="placeholder"
    />
</template>


<script setup lang="ts">
import { computed } from "vue";

interface Props {
    type: string,
    placeholder: string,
    loading:boolean,
    disabled: boolean,
}
const props = defineProps<Props>();

const classes = computed(() => {
    return ["_" + props.type];
});
</script>


<style scoped>
</style>