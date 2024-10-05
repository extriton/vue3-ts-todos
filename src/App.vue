<template>
  <div class="todos-wrap">
    <TodoHeader />
    <TodoFilters :active-filter="activeFilter" @set-filter="setFilter"/>

    <main class="app-main">
      <TodoList
        :todos="filteredTodos"
        @toggle-todo="toggleTodo"
        @remove-todo="removeTodo"
      />
      <TodoAddItem @add-todo="addTodo"/>
    </main>

    <TodoFooter />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TodoHeader from "@/components/todos/TodoHeader.vue";
import TodoFilters from "@/components/todos/TodoFilters.vue";
import TodoList from "@/components/todos/TodoList.vue";
import TodoAddItem from "@/components/todos/TodoAddItem.vue";
import TodoFooter from "@/components/todos/TodoFooter.vue";
import { ITodo } from "@/types/ITodo";
import { TFilter } from "@/types/TFilter";

interface State {
  todos: ITodo[],
  activeFilter: TFilter
}

export default defineComponent({
  components: {
    TodoHeader,
    TodoFilters,
    TodoList,
    TodoAddItem,
    TodoFooter,
  },
  data(): State {
    return {
      todos: [
        { id: 1, text: "Learn the basics of Vue", completed: true },
        { id: 2, text: "Learn the basics of Typescript", completed: false },
        { id: 3, text: "Subscribe to the channel", completed: false },
      ],
      activeFilter: 'All'
    };
  },
  computed: {
    filteredTodos(): ITodo[] { 

      switch (this.activeFilter) {
        case 'Active': 
          return this.todos.filter(todo => !todo.completed)
        case 'Done': 
          return this.todos.filter(todo => todo.completed)
        case 'All':
        default:
          return this.todos
      }

    }
  },
  methods: {
    addTodo(todo: ITodo) {
      this.todos.push(todo)
    },
    toggleTodo(id: number) {
      const targetTodo: ITodo | undefined = this.todos.find((todo: ITodo) => todo.id === id);
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed;
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: ITodo ) => todo.id !== id)
    },
    setFilter(filter: TFilter) {
      this.activeFilter = filter
    }
  },
});
</script>

<style>
.todos-wrap {
  padding: 15px;
  border: 1px solid gray;
  border-radius: 10px;
}
</style>
