<script setup>
const props = defineProps(["todo"]);
const emit = defineEmits(["removeTodo", "changeTodo"]);
</script>

<template>
  <div class="todo-item">
    <input :value="todo.isCompleted" @input="emit('changeTodo')" type="checkbox" />
    <p
      :class="{
        'todo-item__completed': todo.isCompleted,
      }"
    >
      {{ todo.todoText }}
    </p>
    <button class="todo-item__remove" @click="emit('removeTodo')">X</button>
  </div>
</template>

<style scoped lang="scss">
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 300px;
  margin-top: 10px;

  &__remove {
    padding: 3px;
    background: none;
    border: none;
    color: red;
    cursor: pointer;
  }

  &__completed {
    text-decoration: line-through;
    opacity: 0.5;
  }
}
</style>
