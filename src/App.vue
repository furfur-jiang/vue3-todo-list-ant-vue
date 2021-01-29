<template>
  <div class="content">
    <a-card title="备忘录" style="width: 500px">
      <Head :addTodo="addTodo" />
      <List :todos="state.todos"/>
      <Foot
        :checkAllTodo="checkAllTodo"
        :todos="state.todos"
        :delTodoAll="delTodoAll"
      />
    </a-card>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive ,provide,ref} from "vue";
import Head from "./components/Head.vue";
import List from "./components/List.vue";
import Foot from "./components/Foot.vue";
import { ITodo } from "./Type/type";

export default defineComponent({
  name: "App",
  components: {
    Head,
    List,
    Foot,
  },
  setup() {
    const state = reactive<{ todos: ITodo[] }>({
      todos: [
        {
          id: 1,
          title: "furfur-jiang",
          isCompleted: false,
        },
        {
          id: 2,
          title: "棒棒",
          isCompleted: true,
        },
      ],
    });
    const addTodo = (todo: ITodo) => {
      state.todos.unshift(todo);
    };
    const delTodo = (id: number) => {
      const index = state.todos.findIndex((todo) => todo.id == id);
      state.todos.splice(index, 1);
    };
    const delTodoAll = () => {
      state.todos = state.todos.filter((todo) => todo.isCompleted == false);
    };
    // 全选/全不选
    const checkAllTodo = (isCompleted: boolean) => {
      state.todos.forEach((value) => {
        value.isCompleted = isCompleted;
      });
    };
    // 选/不选
    const checkTodo = (id: number, check: boolean) => {
      state.todos.forEach((todo) => {
        if (todo.id == id) {
          todo.isCompleted = check;
        }
      });
    };
    // 跳过list，app与item直接通信，祖孙通信
    provide('delTodo',delTodo)
    provide('checkTodo',checkTodo)
    return {
      state,
      // ...toRefs(state)
      addTodo,
      delTodo,
      checkAllTodo,
      checkTodo,
      delTodoAll,
    };
  },
});
</script>

<style scoped>
.content {
  margin-top: 50px;
  display: flex;
  justify-content: center;
}
</style>
