<script setup>
import TodoItem from "./TodoItem.vue";

const props = defineProps(["todoArr"]);
const emit = defineEmits(["removeTodo", "changeTodo"]);
</script>

<template>
  <div v-if="todoArr.length > 0" class="todo-list">
    <h3>Todo List</h3>
    <TransitionGroup name="list">
      <todo-item
        v-for="todo in todoArr"
        :todo="todo"
        :key="todo.id"
        @removeTodo="emit('removeTodo', todo.id)"
        @changeTodo="emit('changeTodo', todo)"
      />
    </TransitionGroup>
  </div>
  <div v-else class="todo-list todo-list--empty">Todo list is empty</div>
</template>

<style lang="scss" scoped>
.todo-list {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;

  &--empty {
    color: red;
  }
}
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
