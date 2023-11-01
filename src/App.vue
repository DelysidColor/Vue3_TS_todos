<template>
  <Header />
  <Filters :activeFilter="activeFilter" @setFilter="setFilter" />

  <main class="app-main">
    <TodoList
      :todos="filteredTodos"
      @removeTodo="removeTodo"
      @toggleTodo="toggleTodo" />
    <AddTask @addTodo="addTodo" />
  </main>

  <Footer :stats="stats" />
</template>

<script lang="ts">
import { Todo } from "./types/Todo";
import { Filter } from "./types/Filter";
import { defineComponent } from "vue";
import Header from "@/components/Header.vue";
import Filters from "@/components/Filters.vue";
import TodoList from "@/components/TodoList.vue";
import AddTask from "@/components/AddTask.vue";
import Footer, { Stats } from "@/components/Footer.vue";

interface State {
  todos: Todo[];
  activeFilter: Filter;
}

export default defineComponent({
  components: {
    Header,
    Filters,
    TodoList,
    AddTask,
    Footer,
  },
  data(): State {
    return {
      todos: [
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
        {
          id: 0,
          text: "Learn the basics of Typescript",
          completed: true,
        },
      ],
      activeFilter: "All",
    };
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos.unshift(todo);
    },
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id);
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed;
        if (targetTodo.completed) {
          this.todos = this.todos.filter(
            (todo: Todo) => todo.id !== targetTodo.id
          );
          this.todos.push(targetTodo);
        } else {
          this.todos = this.todos.filter(
            (todo: Todo) => todo.id !== targetTodo.id
          );
          this.todos.unshift(targetTodo);
        }
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id);
    },
    setFilter(filter: Filter) {
      this.activeFilter = filter;
    },
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case "Active":
          return this.activeTodos;
        case "Done":
          return this.completedTodos;
        case "All":
        default:
          return this.todos;
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.completedTodos.length,
      };
    },
    activeTodos(): Todo[] {
      return this.todos.filter((todo) => !todo.completed);
    },
    completedTodos(): Todo[] {
      return this.todos.filter((todo) => todo.completed);
    },
  },
});
</script>
