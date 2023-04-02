<template>
    <div class="box todo-add">
        <base-input type="text" id="title" class="todo-add-item title" v-model="title" placeholder="タイトル" maxlength="32" />
        <textarea id="memo" class="todo-add-item" v-model="note" placeholder="メモ"></textarea>
        <base-input type="date" id="limit" class="todo-add-item" v-model="limit" placeholder="期限" />
        <base-button type="add" size="middle"
          class="todo-add-item" 
          @click="onSubmitClick"
          :disabled="isDisabled"
          >
            追加する
        </base-button>
    </div>
</template>


<script setup lang="ts">
import { ref, computed } from "vue";
import type { Ref } from "vue";
import BaseButton from "./BaseButton.vue";
import BaseInput from "./BaseInput.vue";

interface Emits {
    (event: "addNewTodo", title: Ref, note: Ref, limit: Ref): void;
}
const emit = defineEmits<Emits>();

const title = ref("");
const note = ref("");
const limit = ref("");

const isDisabled = computed(() => {
    return title.value === "";
});

const onSubmitClick = () => {
    if (title.value != "") {
        emit("addNewTodo", title, note, limit);
    } else {
        alert("タイトルは必須です．");
    }
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


</style>