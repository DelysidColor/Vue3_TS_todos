<template>
  <ul class="todo-list">
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggleTodo="toggleTodo" />
  </ul>
</template>

<script lang="ts">
import { Todo } from "@/types/Todo";
import { defineComponent } from "vue";
import TodoItem from "@/components/TodoItem.vue";

interface State {
  todos: Todo[];
}

export default defineComponent({
  components: {
    TodoItem,
  },
  data(): State {
    return {
      todos: [
        {
          id: 0,
          text: "Learn the basics of Typescript",
          completed: true,
        },
        {
          id: 1,
          text: "Learn Nuxt",
          completed: false,
        },
        {
          id: 2,
          text: "Find the Job",
          completed: false,
        },
      ],
    };
  },
  methods: {
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id);
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed;
      }
    },
  },
});
</script>
