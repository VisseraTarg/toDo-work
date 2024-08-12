<script setup>
  //import {ref} from "vue";

  const arr = ["abcd","1234","Hello world!","Hello wrld!"]
  const search = 'Hello'
  const regexp = new RegExp(search, "g")

  const doSearch = arr.filter(function(item){
    return item.match(regexp)
  })

  const result = (Boolean(doSearch.length)) ? `${Boolean(doSearch.length)}: ${doSearch}` : `${Boolean(doSearch.length)}`



</script>

<template>
  <div>Дано: {{arr}}</div>
  <div>Найти: {{search}}</div>
  <div>Найдено: {{result}}</div>

</template>

<style scoped>

</style>