<script setup xmlns="http://www.w3.org/1999/html">
import {ref, onMounted, watch, computed} from "vue"
import List from "@/components/List.vue";
import Form from "@/components/Form.vue";

import ForRegExp from "@/components/ForRegExp.vue";
import SearchTest from "@/components/SearchTest.vue";


const todos = ref([])


const isActiveForm = ref(false)

const addTodo = (todo) => {
  isActiveForm.value = false
  todos.value.push(todo)
}

const removeTodo = (todo) => {
  todos.value = todos.value.filter(t => t !== todo)
}

const updateTodo = () => {
  todos.value = todos.value.map(item => {
  if (item.createdAt === todo.createdAt) return todo
    return item
  })
}

const searchInput = ref ('')

//let result = ref()

const searchTodo = computed ((todo)=>{
  todos.value.filter(function (item) {
    return item.content.match(new RegExp(searchInput.value, 'gmi'))
  })

})



const closeForm = () => {
  isActiveForm.value = false
}

watch(todos, newVal => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, {deep: true})

onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})



</script>


<template>
  <main class="app">
    <section class="create-todo">
      <h1>Лист задач</h1>
      <div class="todo-btn" @click="isActiveForm =! isActiveForm">Добавить</div>
      <h3>Список задач</h3>
      <pre>{{todos}}</pre>
      <input type="text" v-model="searchInput" placeholder="Начните вводить название для поиска">

      <Form v-if="isActiveForm" @add="addTodo" @close="closeForm"/>
      <List :list="todos" @remove="removeTodo" @update="updateTodo" />

      <!--<br>
      <br>
      <ForRegExp/>
      <br>
      <br>
      <SearchTest/>-->


    </section>
  </main>
</template>


<style>
*, *:before, *:after {
  box-sizing: border-box;
  font-family: Avantgarde, TeX Gyre Adventor, URW Gothic L, sans-serif;
}
</style>
<style scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  text-align: center;
}

h3 {
  display: block;
  border-bottom: 1px solid grey;
  width: 100%;
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

  margin: 0 auto;
}

.todo-btn:hover {
  background-color: #18da18;
  transition: 0.3s;
}

input[type="text"] {
  padding: 4px 12px;
  outline: #00b600;
  font-size: 16px;
  color: #111;
  border-radius: 8px;
  margin: 0 0 6px;
}
</style>
