<script lang="ts" setup>
let {todoList} = defineProps({
  todoList: Array<string[]>,
})

console.log('todoList', todoList)
</script>

<template>
  <div class="flex flex-col bg-blue-400 shadow-2xl w-1/2 rounded-xl min-h-[500px]" v-if="todoList.length > 0">
      <ul v-for="(todo, key) in todoList" class="flex flex-row p-2 text-white justify-around items-center">
       <li class="p-3" :key="key">
         <label>Item #{{key + 1}} {{todo}}</label>
       </li>
      </ul>
  </div>
</template>
