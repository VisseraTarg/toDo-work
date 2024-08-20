<script setup="">
import Delete from "@/components/Delete.vue";
import Update from "@/components/Update.vue";


const props = defineProps({
  item: Object,
  index: Number,
  isActiveEditForm: Boolean,
})

function makeDone() {
  props.item.done =! props.item.done
}

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
  <div class="todo-item" >

    <label>
      <div class="checkbox" :class="{ done: item.done }">
        <svg width="800px" height="800px" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg" fill="none">
          <path  stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 5L8 15l-5-4"/>
        </svg>
      </div>
      <input type="checkbox" @click="makeDone" v-model="item.done">
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
  margin: 4px;
}
input {
  display: none;
}
svg {
  margin: 10%;
  width: 80%;
  height: 80%;
  stroke: #dadada;
}
.checkbox {
  display: inline-block;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background-color: #dadada;
  margin-bottom: 1px;
  cursor: pointer;
  transition: 0.3s;

}
label:hover .checkbox{
  background-color: #a7dda7;

  transition: 0.3s;
}
label:hover svg{
  stroke: white;

  transition: 0.3s;
}
label:active .checkbox{
  background-color: #00b600;
}

.done {
  background-color: #00b600;
}
.done svg{
  stroke: white;
}

</style>