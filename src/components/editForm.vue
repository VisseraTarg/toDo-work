<script setup="">

import {ref} from "vue";

const emit = defineEmits(['edit'])
const input_content = ref('')
const updateTodo = () => {
  if (input_content.value.trim() === '') {
    return
  }

  emit('edit', {
    content: input_content.value,
    done: false,
    createdAt: new Date().getTime(),
  })
  input_content.value = ''
}
</script>

<template>
  <div class="form_wrapper">
    <form class="form" @submit.prevent="updateTodo">
      <div>Ну довай исправим</div>
      <input
          type="text"
          placeholder="Напиши как надо было"
          v-model="input_content"/>
      <input type="submit" class="todo-btn" value="Сохранить"/>
    </form>
  </div>
</template>

<style scoped>
.form_wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.75);
  padding: 20%;
}
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  row-gap: 20px;
  background-color: #fff;
  padding: 40px;
  border-radius: 16px;
}
input[type="text"] {
  padding: 8px 12px;
  outline: #00b600;
  font-size: 20px;
  color: #111;
  border-radius: 8px;
}
</style>