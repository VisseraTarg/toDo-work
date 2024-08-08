<script setup xmlns="http://www.w3.org/1999/html">
import {ref, onMounted, watch} from "vue"
import List from "@/components/List.vue";
import Form from "@/components/Form.vue";


const todos = ref([])
const name = ref('')

/* some comment */
const isActiveForm = ref(false)

const addTodo = (todo) => {
  isActiveForm.value = false
  todos.value.push(todo)
}

const removeTodo = (todo) => {
  todos.value = todos.value.filter(t => t !== todo)
}

const updateTodo = (todo) => {
  console.log(todo)

}

watch(todos, newVal => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, {deep: true})

watch(name, (newVal) => {
  localStorage.setItem('name', newVal)
})

onMounted(() => {
  name.value = localStorage.getItem('name') || ''
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})


</script>


<template>
  <main class="app">
    <section class="create-todo">
      <h1>Лист задач</h1>
      <div class="todo-btn" @click="isActiveForm =! isActiveForm">Добавить</div>
      <Form v-if="isActiveForm" @add="addTodo"/>
      <List :list="todos" @remove="removeTodo" @update="updateTodo"/>

    </section>
  </main>
</template>


<style>
*, *:before, *:after {
  box-sizing: border-box;
}
</style>
<style scoped>

h3 {
  display: block;
  border-bottom: 1px solid grey;
  width: 100%;
  align-items: center;
}

h1 {
  text-align: center;
}

.todo-btn {
  background-color: #00b600;
  color: #fff;
  text-align: center;
  width: fit-content;
  padding: 12px 20px;
  border: none;
  outline: none;
  border-radius: 8px;
  cursor: pointer;

  transition: 0.3s;
}

.todo-btn:hover {
  background-color: #18da18;
  transition: 0.3s;
}
</style>
