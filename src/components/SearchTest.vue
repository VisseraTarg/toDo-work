<script setup>
import {computed, ref} from "vue";

const arr = ref(["abcd", "1234", "Hello world!", "Hello wrld!"])
//const computedFromArrValue = computed(() => arr.value)
//const computedFirstLast = computed(() => [arr.value[0], arr.value[arr.value.length - 1]])

const newItemOfList = ref('')
const addNewItemOfList = () => {
  arr.value.push(newItemOfList.value)
}

const input_for_search = ref('')
//const regexp = ()

const doSearch = () => {
  const test = arr.value.filter(function (item) {
    return item.match(new RegExp(input_for_search.value, "g"))
  })

}

const search = computed (() => arr.value.filter(function (item) {
  return item.match(new RegExp(input_for_search.value, "g"))
}))

</script>

<template>
  <pre>{{search}}</pre>
  <div>Дано: {{ arr }}</div>
  <input type="text" v-model="newItemOfList"/>
  <input type="submit" value="Добавить в список" @click="addNewItemOfList"/>
  <div>{{ newItemOfList }}</div>
  <br>
  <br>
  <div>Найти {{ input_for_search }}</div>
  <input type="text" v-model="input_for_search">
  <input type="submit" value="Найти" @click="doSearch"/>
  <br>
  <!--  <div>Найдено: {{ doSearch }}</div>-->

</template>

<style scoped>

</style>