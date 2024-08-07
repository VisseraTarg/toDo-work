<script setup="">
import Close from "@/components/Close.vue";
import Update from "@/components/Update.vue";

const props = defineProps({
  item: Object,
  index: Number
})

const emit = defineEmits(['remove', 'update'])

const remove = () => {
  console.log('removed', props.item)
  emit('remove', props.item)
}
const update = () => {
  console.log('updated', props.item)
  emit('update', props.item)
}
</script>

<template>
  <div class="todo-item" :class="{ done: item.done }">
    <label>
      <input type="checkbox"/>
      {{ index + 1 }}. {{ item.content }}
    </label>
    <Close @click="remove"/>
    <Update @click="update"/>
  </div>
</template>

<style scoped>
.todo-item {
  display: flex;
  column-gap: 8px;
  align-items: center;
}
</style>