<script setup>
import { ref } from "vue";

let inputText = ref("");
let emptyErr = ref(false);

const emit = defineEmits(["addTodo"]);

function changeInput(e) {
  inputText.value = e.target.value;
  emptyErr.value = false;
}

function createTodo() {
  if (inputText.value.length > 0) {
    const newTodo = {
      id: Date.now(),
      todoText: inputText.value,
      isCompleted: false,
    };
    emit("addTodo", newTodo);
    inputText.value = "";
    emptyErr.value = false;
  } else {
    emptyErr.value = true;
  }
}
</script>

<template>
  <form @submit.prevent="createTodo" class="todo-header">
    <div class="todo-header__input">
      <input class="todo-header__input-teg" :value="inputText" @input="changeInput" />
      <p v-if="emptyErr" class="todo-header__input-err">Please write text</p>
    </div>
    <button class="todo-header__submit">Add</button>
  </form>
</template>

<style lang="scss" scoped>
.todo-header {
  display: flex;
  justify-content: center;
  height: 30px;
  gap: 10px;

  &__input {
    width: 70%;
    position: relative;

    &-teg {
      width: 100%;
      height: 100%;
    }

    &-err {
      position: absolute;
      bottom: -15px;
      font-size: 0.75rem;
      color: red;
    }
  }
  &__submit {
    padding: 5px;
    cursor: pointer;
  }
}
</style>
