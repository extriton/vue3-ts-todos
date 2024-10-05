<template>
  <ul class="todo-list">
    <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo"/>
  </ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import TodoItem from '@/components/todos/TodoItem.vue';
import { ITodo } from '@/types/ITodo';

export default defineComponent({
  components: {
    TodoItem
  },
  props: {
    todos: {
      type: Object as PropType<ITodo[]>,
      required: true
    }
  }
})
</script>
