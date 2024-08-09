<script setup="">

import ItemOfList from "@/components/ItemOfList.vue";
defineProps({
  list: Array
})

const emit = defineEmits(['remove', 'update'])
const updateList = (item) => {
    emit('update', item)
}

</script>

<template>
  <section class="todo-list">
    <h3>Список задач</h3>
    <div class="list">
      <ItemOfList
          @remove="()=>{emit('remove', item)}"
          @update="updateList"
          v-for="(item, index) in list"
          :item="item" :index="index"
          :key="item.createdAt"
      />
    </div>
  </section>

</template>

<style scoped>
.todo-list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
}
</style>