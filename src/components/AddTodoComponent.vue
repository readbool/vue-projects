<script setup lang="ts">
import {ref} from "vue";

let emit = defineEmits(['handleAddTodo'])

let newTodo = ref(null);

const addTodoTask = () => {
  emit('handleAddTodo', newTodo.value);
  newTodo.value = '';
}

</script>

<template>
  <div class="flex flex-col justify-around items-center w-1/2 shadow-2xl">
    <div class="flex flex-row p-5 gap-4 w-full">
      <div class="flex flex-col w-2/3">
        <input placeholder="Add Todo" class="h-20 w-full rounded-xl p-5" v-model="newTodo"/>
      </div>
      <button
      class="bg-blue-400 text-white rounded-xl w-1/3"
      @click="addTodoTask"
      >Add todo</button>
    </div>
  </div>
</template>
