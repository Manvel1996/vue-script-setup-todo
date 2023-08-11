<script setup>
import TodoHeader from "./TodoHeader.vue";
import TodoList from "./TodoList.vue";

import { ref } from "vue";

const todoArr = ref([]);

function addTodo(todo) {
  todoArr.value.push(todo);
}

function removeTodo(id) {
    console.log("id",id);
  todoArr.value = todoArr.value.filter((el) => el.id !== id);
}

function changeTodo(todo) {
  todoArr.value = todoArr.value.map((el) => {
    if (todo.id === el.id) {
      const newTodo = {
        id: todo.id,
        todoText: todo.todoText,
        isCompleted: !todo.isCompleted,
      };
      return newTodo;
    } else return el;
  });
}
</script>

<template>
  <div class="todo-app">
    <todo-header @addTodo="addTodo" />
    <todo-list :todoArr="todoArr" @changeTodo="changeTodo" @removeTodo="removeTodo" />
  </div>
</template>

<style scoped>
.todo-app {
  margin: 50px auto;
  width: 70%;
  min-height: 200px;
  border: 1px solid teal;
  padding: 15px;
  background: lightGray;
}
</style>
