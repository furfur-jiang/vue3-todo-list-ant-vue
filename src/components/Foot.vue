<template>
  <div class="foot">
    <div>
      <input
        type="checkbox"
        v-model="ischeckAll"
        id="checkAll"
        @click="checkAllFun"
      />
      <label for="checkAll"> 已完成{{ count }} / 全部{{ todos.length }}</label>
    </div>
    <a-button type="danger" @click="delAll">删除选中</a-button>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed } from "vue";
import { ITodo } from "../Type/type";

export default defineComponent({
  name: "Foot",
  props: {
    checkAllTodo: {
      type: Function,
      required: true,
    },
    delTodoAll: {
      type: Function,
      required: true,
    },
    todos: {
      type: Array as () => ITodo[],
    },
  },
  setup(props) {
    // 统计已完成
    const count = computed(() => {
      return (
        props.todos &&
        props.todos.reduce((pre, todo) => pre + (todo.isCompleted ? 1 : 0), 0)
      );
    });
    // 全选与否
    const ischeckAll = computed({
      get() {
        return (
          (count.value || 0) > 0 && count.value == (props.todos || []).length
        );
      },
      set(val) {
        props.checkAllTodo(val);
      },
    });

    const delAll = () => {
      props.delTodoAll();
    };
    return {
      ischeckAll,
      delAll,
      count,
    };
  },
});
</script>

<style scoped>
.foot {
  margin-top: 15px;
  display: flex;
  justify-content: space-between;
}
</style>
