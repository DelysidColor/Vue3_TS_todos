<template>
  <Header />
  <Filters />

  <main class="app-main">
    <TodoList />
    <AddTask />
  </main>

  <Footer />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Header from "@/components/Header.vue";
import Filters from "@/components/Filters.vue";
import TodoList from "@/components/TodoList.vue";
import AddTask from "@/components/AddTask.vue";
import Footer from "@/components/Footer.vue";

export default defineComponent({
  components: {
    Header,
    Filters,
    TodoList,
    AddTask,
    Footer,
  },
});
</script>
