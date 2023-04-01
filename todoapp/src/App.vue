<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" />
    <h1 id="title">TodoAppWithVue</h1>
  </header>

  <main class="main-content">
      <todo-add @addNewTodo="addNewTodo"></todo-add>

      <br>
      
      <todo-task v-for="[id, td] in todoList" 
        :key="id" 
        :id="td.id" 
        :title="td.title" 
        :note="td.note" 
        :limit="td.limit"
        @delete-button-clicked="deleteTodo">
      </todo-task>
  </main>

  <footer>
  </footer>
</template>


<script setup lang="ts">
import { ref } from "vue";
import type { Ref } from "vue";
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

const addNewTodo = (title: Ref, note: Ref, limit: Ref) => {
  idcnt++;
  todoList.value.set(idcnt, { id: idcnt, title: title.value, note: note.value, limit: limit.value });
  title.value = "";
  note.value = "";
  limit.value = "";
}

const deleteTodo = (id: number, title: string) => {
  if (confirm(title + "を削除しますか？")) {
    todoList.value.delete(id);
  }
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
  border: green 1px solid;
  line-height: 1.5;
  height: 64px;
}

#title {
  display: block;
  text-align: center;
  margin: 0 auto;
}

.logo {
  display: block;
  margin: 0 auto;
  width: 48px;
  height: 48px;
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

  #title {
    margin: 0 0;
  }
}

footer {
  width: 100%;
  height: auto;
  padding: 5%;
  background-color: bisque;
  position: absolute;
  bottom: 0;
}
</style>
