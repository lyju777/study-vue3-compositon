<template>
  <TodoHeader></TodoHeader>
  <TodoInput @add="addTodoItem"></TodoInput>
  <TodoList :todoItems="todoItems" @remove="removeTodoItem"></TodoList>
</template>

<script>
import { ref } from "vue";
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";

export default {
  components: { TodoHeader, TodoInput, TodoList },

  setup() {
    const todoItems = ref([]);

    function fetchTodos() {
      const result = [];
      for (let i = 0; i < localStorage.length; i++) {
        const todoItem = localStorage.key(i);
        // items.value.push(todoItem);
        result.push(todoItem);
      }
      return result;
    }

    todoItems.value = fetchTodos();

    function addTodoItem(todo) {
      todoItems.value.push(todo);
      localStorage.setItem(todo, todo);
    }

    return { todoItems, addTodoItem };
  },
  methods: {
    removeTodoItem(item, index) {
      this.todoItems.splice(index, 1);
      localStorage.removeItem(item);
    },
  },
};
</script>

<style lang="scss" scoped></style>
