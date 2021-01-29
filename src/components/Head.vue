<template>
  <div class="Head">
    <input
      v-model="title"
      placeholder="请输入你的任务，并按回车确认"
      @keyup.enter="add"
      allowClear
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "Head",
  props: {
    addTodo: {
      type: Function,
      required: true,
    },
  },
  setup(props) {
    const title = ref("");
    const add = () => {
      const text = title.value;
      if (!text.trim()) return;
      const todo = {
        id: Date.now(),
        title: text,
        isCompleted: false,
      };
      props.addTodo(todo);
      title.value = "";
    };
    return {
      title,
      add,
    };
  },
});
</script>

<style scoped>
input {
  width: 100%;
  margin-bottom: 15px;
}
</style>
