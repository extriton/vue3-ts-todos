<template>
  <section class="add-todo">
    <form v-if="isFormVisible" class="add-todo__form" @submit.prevent="addTodo">
      <button class="close-button" type="button" @click="hideForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button
      v-else
      type="submit"
      class="add-todo__show-form-button"
      @click="showForm"
    >
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { ITodo } from "@/types/ITodo";

interface State {
  todoText: string;
  isFormVisible: boolean;
}

export default defineComponent({
  data(): State {
    return {
      todoText: "",
      isFormVisible: false,
    };
  },
  methods: {
    addTodo() {
      if (!this.todoText) {
        return;
      }
      this.$emit("addTodo", {
        id: Date.now(),
        text: this.todoText,
        completed: false
      });
      this.todoText = "";
    },
    showForm() {
      this.isFormVisible = true;
    },
    hideForm() {
      this.isFormVisible = false;
    },
  },
  emits: {
    addTodo: (todo: ITodo) => todo
  },
});
</script>
