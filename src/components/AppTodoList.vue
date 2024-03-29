<template>
  <ul class="todo-list">
    <AppTodoItem @remove-todo="removeTodo" @toggle-todo="toggleTodo" v-for="item in todos" :key="item.id"
      :todo="item" />
  </ul>
</template>
<script lang="ts">
import { defineComponent, PropType } from "vue";
import AppTodoItem from "./AppTodoItem.vue";
import { Todo } from "@/models/Todo";


export default defineComponent({
  components: {
    AppTodoItem
  },
  props: {
    todos: {
      type: Array as PropType<Todo[]>
    }
  },
  methods: {
    toggleTodo(id: number) {
      this.$emit("toggleTodo", id)
    },
    removeTodo(id: number) {
      this.$emit("removeTodo", id)
    }
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  }

})
</script>