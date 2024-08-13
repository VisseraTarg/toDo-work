<script setup>
  //import {ref} from "vue";

  const arr = ["abcd","1234","Hello world!","Hello wrld!"]
  const search = 'Hell'
  const regexp = new RegExp(search, "g")

  const doSearch = arr.filter(function(item){
    return item.match(regexp)
  })

  const result = (Boolean(doSearch.length)) ? `${Boolean(doSearch.length)}: ${doSearch}` : `${Boolean(doSearch.length)}`



</script>

<template>
  <div>Дано: {{arr}}</div>
  <br>
  <div>Найти: {{search}}</div>
  <br>
  <div>Найдено: {{result}}</div>

</template>

<style scoped>

</style>