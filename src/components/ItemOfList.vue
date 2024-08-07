<script setup="">
import Close from "@/components/Close.vue";
import Update from "@/components/Update.vue";
import editForm from "@/components/editForm.vue";
import {ref} from "vue";

const props = defineProps({
  item: Object,
  index: Number
})

const emit = defineEmits(['remove', 'update'])

const remove = () => {
  console.log('removed', props.item)
  emit('remove', props.item)
}
const isActiveEditForm = ref(false)
const update = () => {
  console.log('updated', props.item)
  isActiveEditForm.value = false
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
    <editForm v-if="isActiveEditForm" @edit="update"/>
  </div>
</template>

<style scoped>
.todo-item {
  display: flex;
  column-gap: 8px;
  align-items: center;
}
</style>