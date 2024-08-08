<script setup="">
import Close from "@/components/Close.vue";
import Update from "@/components/Update.vue";
import {computed, ref} from "vue";
import editForm from "@/components/editForm.vue";



const props = defineProps({
  item: Object,
  index: Number
})

const emit = defineEmits(['remove', 'update'])

const edited_value = computed(()=> props.item.content)

const remove = () => {
  console.log('removed', props.item)
  emit('remove', props.item)
}

const isActiveEditForm = ref(false)

const update = () => {
  isActiveEditForm.value = false
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

    <Update @click="isActiveEditForm =! isActiveEditForm"/>
    <editForm v-if="isActiveEditForm" @update="update" v-model="edited_value"/>
    <Close @click="remove"/>


  </div>
</template>

<style scoped>
.todo-item {
  display: flex;
  column-gap: 8px;
  align-items: center;
}
</style>