<script setup="">
import {ref} from "vue";

import Close from "@/components/Close.vue";

const emit = defineEmits(['add','close']) //

const input_content = ref('')
const addTodo = () => {
  if (input_content.value.trim() === '') {
    return
  }

  emit('add', {
    content: input_content.value,
    done: false,
    createdAt: new Date().getTime(),
  })
  input_content.value = ''
}

const close = () => {
  emit ('close')
}

const fillFields = {
    placeholderText: "Назови задачу",
  }


</script>

<template>
  <div class="form_wrapper">

    <form class="form" @submit.prevent="addTodo">
      <Close @click="close"/>
      <div>Ну довай добавим</div>
      <input
          type="text"
          v-bind:placeholder="fillFields.placeholderText"
          v-model="input_content"/>
      <input type="submit" class="todo-btn" value="Добвить"/>

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
  padding: 15%;
}
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  row-gap: 20px;
  background-color: #fff;
  padding: 10%;
  border-radius: 16px;
  position: relative;
}
input[type="text"] {
  padding: 8px 12px;
  outline: #00b600;
  font-size: 20px;
  color: #111;
  border-radius: 8px;
  width: 100%;
}
</style>