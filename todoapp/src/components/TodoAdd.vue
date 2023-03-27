<template>
    <div class="box todo-add">
        <input type="text" id="title" class="todo-add-item" v-model="title" placeholder="タイトル" maxlength="32">
        <textarea id="memo" class="todo-add-item" v-model="note" placeholder="メモ"></textarea>
        <input type="date" id="limit" class="todo-add-item" v-model="limit" placeholder="期限">
        <button id="add-button" class="todo-add-item" @click="onSubmitClick">追加する</button>
    </div>
</template>


<script setup lang="ts">
import { ref, computed, type Ref } from "vue";
interface Emits {
    (event: "addNewTodo", title: string, note: string, limit: string): void;
}
const emit = defineEmits<Emits>();

const title = ref("");
const note = ref("");
const limit = ref("");

const onSubmitClick = () => {
    emit("addNewTodo", title.value, note.value, limit.value);
}

</script>


<style scoped>
.todo-add {
    padding: 10px 0;
    flex-direction: column;
    width: auto;
    height: 200px;
}

.todo-add-item {
    margin: 3px 0;
    width: 80%;
}

#memo {
    height: 50%;
}

#add-button {
    position: relative;
}

input[type=date]::-webkit-calendar-picker-indicator {

    width: 100%;
    height: 100%;
    opacity: 0;
}

input[type=date]::-webkit-inner-spin-button {
    -webkit-appearance: none;
}

input[type=date]::-webkit-clear-button {
    -webkit-appearance: none;
}
</style>