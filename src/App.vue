<template>
  <button @click="postMessage">postMessage</button>
  <ul>
    <li v-for="(item, i) in msgList" :key="i">
      {{ item }}
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";
import Worker from "./worker?worker";

export default defineComponent({
  setup() {
    const worker = new Worker();
    const msgList = reactive<string[]>([]);

    worker.onmessage = (e) => {
      msgList.push(e.data);
    };

    function postMessage() {
      worker.postMessage("Hello, world");
    }

    return {
      postMessage,
      msgList,
    };
  },
});
</script>

<style></style>
