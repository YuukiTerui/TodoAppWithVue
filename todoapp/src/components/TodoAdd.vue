<template>
    <div class="box todo-add">
        <input type="text" class="todo-add-item" v-model="title" placeholder="タイトル">
        <textarea class="todo-add-item" v-model="note" rows="5" cols="22" placeholder="メモ"></textarea>
        <input type="date" class="todo-add-item" v-model="limit">
        <button class="todo-add-item" @click="onSubmitClick">追加する</button>
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
}

.todo-add-item {
    margin: 3px 0;
    width: 60%;
}
</style>