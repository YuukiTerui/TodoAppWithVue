<template>
    <section class="box">
        <div class="todo-info">
            <div id="id" hidden>
                {{ id }}
            </div>
            <details width="100%">
                <summary id="title">
                    {{ title }}
                </summary>
                <div id="note" v-html="localNote"></div>
            </details>
            <div id="limit">
                {{ localLimit }}
            </div>
        </div>
        <div class="todo-edit">
            <base-button type="delete" size="small" @click="deleteButtonClicked">削除</base-button>
        </div>
    </section>
</template>


<script setup lang="ts">
import { ref, computed } from "vue";
import BaseButton from "./BaseButton.vue";

interface Props {
    id: number;
    title?: string;
    note?: string;
    limit?: string;
}
const props = withDefaults(
    defineProps<Props>(),
    // なんか効かないので，computedする．おそらく空文字が入っているせい．
    {
        title: "無題",
        note: "--",
        limit: "期限なし"
    }
)

const localNote = computed(() => {
    let localNote = props.note;
    if (localNote !== "") {
        localNote = localNote.replace(/\n/g, "<br>");
    } else {
        localNote = "---";
    }
    return localNote;
});

const localLimit = computed(() => {
    let localLimit = props.limit;
    if (localLimit === "") {
        localLimit = "期限なし";
    }
    return localLimit;
})

interface Emits {
    (event: "deleteButtonClicked", id: number, title: string): void
}
const emit = defineEmits<Emits>();

const deleteButtonClicked = () => {
    emit("deleteButtonClicked", props.id, props.title);
}

</script>


<style scoped>
.box {
    width: 100%;

}

.todo-info {
    padding-left: 10px;
    width: 80%;
}

.todo-edit {
    width: 20%;
}

#note {
    width: 100%;
    overflow-wrap: break-word;
}

#delete-btn {
    margin: 0 0 0 auto;
}
</style>