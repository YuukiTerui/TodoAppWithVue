<template>
    <input 
        :type="type"
        class="BaseInput"
        :class="classes"
        :disabled="disabled || loading"
    />
</template>


<script setup lang="ts">
import { computed } from "vue";

interface Props {
    type: string,
    loading:boolean,
    disabled: boolean,
}
const props = withDefaults(
    defineProps<Props>(),
    {
        type: "text",
        loading: false,
        disabled: false
    }
);

const classes = computed(() => {
    return ["_" + props.type];
});
</script>


<style scoped>
._date {
    position: relative;
}
._date::-webkit-calendar-picker-indicator {
    position: absolute;
    width: 100%;
    height: 100%;
    opacity: 0;
    cursor: pointer;

}
._date::-webkit-inner-spin-button {
    -webkit-appearance: none;
}
._date::-webkit-clear-button {
    -webkit-appearance: none;
}
</style>