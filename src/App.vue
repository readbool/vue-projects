<script setup lang="ts">
import {ref} from "vue";
import AddTodoComponent from "./components/AddTodoComponent.vue";
import TodoListingComponent from "./components/TodoListingComponent.vue";

let todoList = ref([]);

const handleAddTodo = (addedTodo) => {
  todoList.value.push(addedTodo);
}

const handleRemoveTodo = (index) => {
  todoList.value.splice(index, 1);
}

</script>

<template>
  <div class="bg-blue-950 h-screen w-full">
    <div class="flex flex-row mx-10 justify-center items-center">
    <add-todo-component @handleAddTodo="handleAddTodo"/>
    </div>
    <div class="flex flex-row mx-10 justify-center items-center">
     <TodoListingComponent :todo-list="todoList" @handle-remove-todo="handleRemoveTodo"/>
    </div>
  </div>
</template>

<style scoped>
</style>
