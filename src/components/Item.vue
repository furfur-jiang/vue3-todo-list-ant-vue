<template>
  <li class="li-item">
    <div class="input-item">
      <input
        type="checkbox"
        :id="todo.id"
        :checked="todo.isCompleted"
        @click="check(todo.id, !todo.isCompleted)"
      />
      <label :for="todo.id">{{ todo.title }}</label>
    </div>
    <a-button type="danger" @click="del(todo.id)">删除</a-button>
  </li>
</template>

<script lang="ts">
import { defineComponent, inject } from "vue";
import { ITodo } from "../Type/type";
export default defineComponent({
  name: "Item",
  props: {
    todo: {
      type: Object as () => ITodo,
    }
  },
  setup(props) {
    const delTodo: Function | undefined = inject("delTodo");
    const checkTodo: Function | undefined = inject("checkTodo");
    
    const del = (id: number) => {
      (delTodo as Function)(id);
    };
    const check = (id: number, check: boolean) => {
      (checkTodo as Function)(id, check);
    };

    return {
      del,
      check,
    };
  },
});
</script>

<style scoped>
.li-item {
  display: flex;
  justify-content: space-between;
  margin-top: 5px;
}
</style>
