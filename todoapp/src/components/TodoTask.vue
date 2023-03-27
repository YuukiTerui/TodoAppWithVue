<template>
    <section class="box">
        <div class="todo-info">
            <div class="id" hidden>
                {{ id }}
            </div>
            <details>
                <summary class="title">
                    {{ localTitle }}
                </summary>
                <div class="note">
                    {{ note }}
                </div>
            </details>
            <div class="limit">
                {{ localLimit }}
            </div>
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

const localLimit = computed(() => {
    let localLimit = props.limit;
    if (localLimit === "") {
        localLimit = "期限なし";
    }
    return localLimit;
})


</script>


<style scoped>
.box {
  border: green 1px solid;
  margin: 10px 30%;
  font-family: "Kokoro", "Vollkorn";
  display: flex;
  place-items: center;
}
</style>