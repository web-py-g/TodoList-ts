<template>
  <AppHeader />
  <AppFilters :active-filter="activeFilter" @set-filter="setFilter" />

  <main class="app-main">
    <AppTodoList :todos=filteredTodos @remove-todo="removeTodo" @toggle-todo="toggleTodo" />

    <AppAddTodo @add-todo="addTodo" />
  </main>

  <AppFooter :stats="stats" />
</template>

<script lang="ts">
import AppHeader from "@/components/AppHeader.vue";
import AppFilters from "@/components/AppFilters.vue";
import AppTodoList from "@/components/AppTodoList.vue";
import AppAddTodo from "@/components/AppAddTodo.vue";
import AppFooter, { Stats } from "@/components/AppFooter.vue";
import { Todo } from '@/models/Todo';
import { Filter } from '@/models/Filter';

import { defineComponent } from "vue";

interface State {
  todos: Todo[],
  activeFilter: Filter
}

export default defineComponent({
  name: "App",
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
  },
  data(): State {
    return {
      todos: [
        { id: 0, text: 'Посмотреть обучалку', complited: true },
        { id: 1, text: 'Создать проект', complited: false },
        { id: 2, text: 'Выучить  TypeScript', complited: false },
        { id: 3, text: "Изучить еще что-то", complited: false }
      ],
      activeFilter: "All"
    }
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case "Active":
          return this.activeTodos
        case "Done":
          return this.doneTodos
        case "All":
        default:
          return this.todos
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length,
      }
    },
    activeTodos(): Todo[] {
      return this.todos.filter(el => !el.complited)
    },
    doneTodos(): Todo[] {
      return this.todos.filter(el => el.complited)
    }
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos.push(todo);
    },
    toggleTodo(id: number) {
      let todo = this.todos.find((el: Todo) => el.id === id);
      if (todo) {
        todo.complited = !todo.complited
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((el: Todo) => el.id !== id);
    },
    setFilter(value: Filter) {
      this.activeFilter = value
    }
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
