<template>
    <section class="box">
        <div class="todo-info">
            <div id="id" hidden>
                {{ id }}
            </div>
            <details>
                <summary id="title">
                    {{ localTitle }}
                </summary>
                <div id="note" v-html="localNote">
                </div>
            </details>
            <div id="limit">
                {{ localLimit }}
            </div>
        </div>
        <div class="todo-edit">
            <button type="button" @click="deleteButtonClicked">削除</button>
        </div>
    </section>
</template>


<script setup lang="ts">
import { ref, computed } from "vue";

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
const localTitle = computed(() => {
    let localTitle = props.title;
    if (localTitle === "") {
        localTitle = "無題";
    }
    return localTitle;
});

const localNote = computed(() => {
    let localNote = props.note;
    localNote = localNote.replace(/\n/g, "<br>");
    console.log(localNote)
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

.todo-info {
    padding-left: 10px;
}

.todo-edit {
    margin: 0 5% 0 auto;
}
</style>