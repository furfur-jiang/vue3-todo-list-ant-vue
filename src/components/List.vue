<template>
  <ul class="List">
    <Item
      v-for="todo in todos"
      :key="todo.id"
      :id="id"
      :todo="todo"
      :delTodo="delTodo"
      :checkTodo="checkTodo"
    />
  </ul>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";
import Item from "./Item.vue";
export default defineComponent({
  name: "List",
  components: {
    Item,
  },
  props: {
    todos: {
      type: Array,
      required: true,
    }
  }
});
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0
}
</style>
