<template>
  <ul class="todo-list">
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggleTodo="toggleTodo"
      @removeTodo="removeTodo" />
  </ul>
</template>

<script lang="ts">
import { Todo } from "@/types/Todo";
import { defineComponent, PropType } from "vue";
import TodoItem from "@/components/TodoItem.vue";

export default defineComponent({
  components: {
    TodoItem,
  },
  props: {
    todos: {
      type: Array as PropType<Todo[]>,
      required: true,
    },
  },
  methods: {
    toggleTodo(id: number) {
      this.$emit("toggleTodo", id);
    },
    removeTodo(id: number) {
      this.$emit("removeTodo", id);
    },
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  },
});
</script>
