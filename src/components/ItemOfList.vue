<script setup="">
import Delete from "@/components/Delete.vue";
import Update from "@/components/Update.vue";


const props = defineProps({
  item: Object,
  index: Number,
  isActiveEditForm: Boolean,
})

const emit = defineEmits(['remove', 'openEditForm'])

const remove = () => {
  console.log('removed', props.item)
  emit('remove', props.item)
}

const openEditForm = () => {
  emit('openEditForm', props.item)
}

</script>

<template>
  <div class="todo-item" :class="{ done: item.done }">
    <label>
      <input type="checkbox"/>
      {{ index + 1 }}. {{ item.content }}
    </label>

    <Update @click="openEditForm"/>

    <Delete @click="remove"/>
  </div>
</template>

<style scoped>
.todo-item {
  display: flex;
  column-gap: 8px;
  align-items: center;
}
</style>