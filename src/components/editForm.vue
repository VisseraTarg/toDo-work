<script setup="">
//import Form from "@/components/Form.vue"; ???
import {ref} from "vue";

import Close from "@/components/Close.vue";


const props = defineProps({
  edited_value: String
})
const emit = defineEmits(['updateEditedModel','close'])

const updateTodo= () => {
  emit('updateEditedModel', edited.value)
}

const edited = ref(props.edited_value || '')

const close = () => {
  emit ('close')
}


</script>

<template>
  <div class="form_wrapper">
    <form class="form" @submit.prevent="updateTodo">
      <Close @click="close"/>
      <div>Ну довай исправим</div>
      <input
          type="text"
          v-model="edited"
      />
      <input type="submit" class="todo-btn" value="Исправить"/>
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
  position: relative;
}
input[type="text"] {
  padding: 8px 12px;
  outline: #00b600;
  font-size: 20px;
  color: #111;
  border-radius: 8px;
}

</style>