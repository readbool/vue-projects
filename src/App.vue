<script setup lang="ts">
import {ref} from "vue";
import AddTodoComponent from "./components/AddTodoComponent.vue";
import TodoListingComponent from "./components/TodoListingComponent.vue";

let todoList = ref([]);

const handleAddTodo = (addedTodo) => {
  todoList.value.push(addedTodo);
}

</script>

<template>
  <div class="bg-blue-950 h-screen w-full">
    <div class="flex flex-row mx-10 justify-center items-center">
    <add-todo-component @handleAddTodo="handleAddTodo"/>
    </div>
    <div class="flex flex-row mx-10 justify-center items-center">
     <TodoListingComponent :todo-list="todoList" />
    </div>
  </div>
</template>

<style scoped>
</style>
