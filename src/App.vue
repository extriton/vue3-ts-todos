<template>
<div class="todos-wrap">
  
  <TodoHeader />
  <TodoFilters />

  <main class="app-main">
    <TodoList :todos="todos"/>
    <TodoAddItem />
  </main>

  <TodoFooter />

</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import TodoHeader from '@/components/todos/TodoHeader.vue'
import TodoFilters from '@/components/todos/TodoFilters.vue';
import TodoList from '@/components/todos/TodoList.vue';
import TodoAddItem from '@/components/todos/TodoAddItem.vue';
import TodoFooter from '@/components/todos/TodoFooter.vue';
import { ITodo } from '@/types/ITodo';

interface State {
  todos: ITodo[]
}

export default defineComponent({
  components: {
    TodoHeader,
    TodoFilters,
    TodoList,
    TodoAddItem,
    TodoFooter
  },
  data(): State {
    return {
      todos: [
        { id: 1, text: 'Learn the basics of Vue', completed: true },
        { id: 2, text: 'Learn the basics of Typescript', completed: false },
        { id: 3, text: 'Subscribe to the channel', completed: false },
        { id: 4, text: 'Subscribe to the channel222', completed: false }
      ]
    }
  }
})

</script>

<style>
.todos-wrap {
  padding: 15px;
  border: 1px solid gray;
  border-radius: 10px;
}
</style>
