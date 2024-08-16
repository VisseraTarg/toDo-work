<script setup="">
import Delete from "@/components/Delete.vue";
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

const update = (edited) => {
  isActiveEditForm.value = false
  emit('update', {
    done: props.item.done,
    content: edited,
    createdAt: props.item.createdAt,
  })
}

const closeModal = (edited) => {
  isActiveEditForm.value = false

}

</script>

<template>
  <div class="todo-item" :class="{ done: item.done }">
    <label>
      <input type="checkbox"/>
      {{ index + 1 }}. {{ item.content }}
    </label>

    <Update @click="isActiveEditForm =! isActiveEditForm"/>
    <editForm
        v-if="isActiveEditForm"
        @updateEditedModel="update"
        @close="closeModal"
        :edited_value="edited_value"/>
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