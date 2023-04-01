<template>
    <button type="button" class="BaseButton" :class="classes" :disabled="disabled || loading" @click="$emit('click')">
        <span v-if="loading">読み込み中</span>
        <slot v-else></slot>
    </button>
</template>

<script setup lang="ts">
import { computed } from "vue";

interface Props {
    type: string,
    size: string,
    loading: boolean,
    disabled: boolean,
}
const props = withDefaults(
    defineProps<Props>(),
    {
        type: "default",
        size: "middle",
        loading: false,
        disabled: false,
    }
);

const classes = computed(() => {
    return ["_" + props.type, "_" + props.size];
});
</script>

<style scoped>
.BaseButton {
    appearance: none;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    height: 32px;
    width: auto;
    padding: 0 16px;
    border: gray solid 1px;
    border-radius: 2rem;
    font-size: 12;
    opacity: .8;
    cursor: pointer;
}

.BaseButton:hover {
    border-color: black;
    opacity: 1;
}

.BaseButton:disabled {
    cursor: not-allowed;
}

/* type */
.BaseButton._small {
    height: 24px;
    font-size: 10px;
}

.BaseButton._middle {
    height: 32px;
    font-size: 12px;
}

.BaseButton._large {
    height: 40px;
    font-size: 14px;
}

/* type */
.BaseButton._default {
    background-color: lightgray;
    color: black;
}

.BaseButton._add {
    background-color: green;
    color: aliceblue;
}

.BaseButton._add:disabled {
    background-color: rgb(90, 145, 90);
    color: lightgray;
}

.BaseButton._delete {
    background-color: olivedrab;
    color: aliceblue;
}





</style>