<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" />
    <div class="wrapper">

      <h1>TodoAppWithVue</h1>
    </div>
  </header>

  <main class="main-content">
      <todo-add @add-new-todo="addNewTodo"></todo-add>

      <todo-task v-for="[id, td] in todoList" 
        :key="id" 
        :id="td.id" 
        :title="td.title" 
        :note="td.note" 
        :limit="td.limit"
        @delete-button-clicked="deleteTodo">
      </todo-task>
  </main>
</template>


<script setup lang="ts">
import { ref } from "vue";
import TodoTask from "./components/TodoTask.vue";
import TodoAdd from "./components/TodoAdd.vue";

interface todo {
  id: number;
  title: string;
  note: string;
  limit: string
}
const todoListInit = new Map<number, todo>();
todoListInit.set(1, { id: 1, title: "test1", note: "メモ1", limit: new Date().toDateString() });
todoListInit.set(2, { id: 2, title: "test2", note: "メモ2", limit: new Date().toDateString() });
let idcnt = todoListInit.size;
const todoList = ref(todoListInit);

const addNewTodo = (title: string, note: string, limit: string) => {
  idcnt++;
  todoList.value.set(idcnt, { id: idcnt, title: title, note: note, limit: limit });
}

const deleteTodo = (id: number, title: string) => {
  todoList.value.delete(id);
}
</script>


<style scoped>
.main-content {
  margin: 10px 20%;
  border: black 1px solid;
}
.box {
  border: green 1px solid;
  font-family: "Kokoro", "Vollkorn";
  display: flex;
  place-items: center;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
  width: 64px;
  height: 64px;
}

@media (min-width: 800px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
