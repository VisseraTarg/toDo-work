<script setup xmlns="http://www.w3.org/1999/html">
import {computed, onMounted, ref, watch} from "vue"

import Form from "@/components/Form.vue";
import ItemOfList from "@/components/ItemOfList.vue";
import editForm from "@/components/editForm.vue";

const todos = ref([])
const isActiveForm = ref(false)
const searchInput = ref('')
const isActiveEditForm = ref(false)
const editedTodo = ref()

const searchTodo = computed((todo) =>
    todos.value.filter((item) =>
        item.content.match(new RegExp(searchInput.value, 'gmi')) //done = false
    ))

const addTodo = (todo) => {
  isActiveForm.value = false
  todos.value.push(todo)
}

const removeTodo = (todo) => {
  todos.value = todos.value.filter(t => t !== todo)
}

const updateEditedModel = (content) => {
  todos.value = todos.value.map(item => {
    if (item.createdAt === editedTodo.value.createdAt)
      return {
        content,
        done: editedTodo.value.done,
        createdAt: editedTodo.value.createdAt
      }
    return item
  })
  isActiveEditForm.value = false
}

const openEditTodoForm = (editValue) => {
  isActiveEditForm.value = true
  editedTodo.value = editValue
}

const closeModal = (edited) => {
  isActiveEditForm.value = false
}

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
      <input type="text" v-model="searchInput" placeholder="Начните вводить название для поиска">
      <h3>Список задач</h3>
      <Form v-if="isActiveForm"
            @add="addTodo"
            @close="closeForm"/>
      <editForm
          v-if="isActiveEditForm"
          @update="updateEditedModel"
          @close="closeModal"
          :edited_value="editedTodo.content"
      />
      <section class="todo-list">
        <div class="list">
          <ItemOfList
              @remove="removeTodo"
              @openEditForm="openEditTodoForm"
              v-for="(item, index) in searchTodo"
              :item="item" :index="index"
              :key="item.createdAt"
          />
        </div>
      </section>
      <h3>Список выполненных задач</h3>
      <pre>{{searchTodo}}</pre>
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
  width: 100%;
}

.todo-list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
}
</style>
