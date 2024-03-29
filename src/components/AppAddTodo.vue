<template>
  <section class="add-todo">
    <button class="add-todo__show-form-button" v-if="!isFormVisible" @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
    <form @submit.prevent="addTodo" class="add-todo__form" v-else>
      <button class="close-button" type="button" @click="hideForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
  </section>
</template>
<script lang="ts">
import { Todo } from '@/models/Todo';
import { defineComponent } from 'vue';

interface State {
  isFormVisible: boolean,
  todoText: string
}


export default defineComponent({
  data(): State {
    return {
      isFormVisible: false,
      todoText: ""
    }
  },
  methods: {
    showForm() {
      this.isFormVisible = true
    },
    hideForm() {
      this.isFormVisible = false
    },
    addTodo() {
      this.$emit("addTodo", {
        id: Date.now(),
        text: this.todoText,
        complited: false
      })

      this.todoText = ""
    }
  },
  emits: {
    addTodo: (todo: Todo) => todo
  }
})

</script>