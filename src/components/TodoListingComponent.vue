<script lang="ts" setup>
import {ref} from "vue";

let {todoList} = defineProps({
  todoList: Array<string[]>,
})

let emit = defineEmits(['handleRemoveTodo']);

let inputDisabled = ref(true);

const handleRemoveTodo = (index: number) => {
  emit('handleRemoveTodo', index)
}

const toggleDisable = () => {
  inputDisabled.value = !inputDisabled.value;
}

</script>

<template>
  <div class="flex flex-col bg-blue-400 shadow-2xl w-1/2 rounded-xl min-h-[500px]" v-if="todoList.length > 0">
      <ul v-for="(todo, key) in todoList" class="flex flex-row p-2 text-white justify-around items-center">
       <li class="p-3 flex flex-col" :key="key">
         <div class="flex flex-row items-center justify-center gap-3 border px-5 py-3  rounded-xl" @dblclick="toggleDisable">
           <label class="font-semibold" @dblclick="toggleDisable">Item #{{key + 1}}</label>
           <input :class="inputDisabled ? 'font-bold bg-transparent h-10 w-60 z-50' :'font-bold' "
                  :value="todo" :disabled="inputDisabled"/>
           <button class="bg-red-600 rounded-xl px-2 py-2"
           @click="handleRemoveTodo(key)"
           > Remove </button>
         </div>
       </li>
      </ul>
  </div>
</template>
