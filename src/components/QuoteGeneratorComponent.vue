<script setup lang="ts">
import {onMounted, ref} from "vue";
import {useFetch} from "../libs/fetch.ts";

let emit = defineEmits(['handleGetQuote']);

let quoteList = ref(null);

onMounted(async () => {
  quoteList = await useFetch('https://dummyjson.com/quotes?limit=100').data;
})

const handleOnClick = async () => {
  const randomNumber = Math. floor(Math. random() * 100) + 1;
  let list = quoteList.value;

  if (!list) {
    list = await useFetch('https://dummyjson.com/quotes?limit=100').data;
  }

  let filtered = list.quotes.filter((quote) => {
    if(quote.id === randomNumber) {
      return quote;
    }
  })[0];

  emit('handleGetQuote', filtered)
}

</script>

<template>
<div class="
flex
flex-col
w-full
h-full
justify-center
items-center
gap-5
bg-green-600
text-white
my-10
rounded-xl
shadow-gray-300
p-5
">
  <div class="flex flex-row items-center justify-center p-5">
    <h1 class="text-6xl">The Quote Generator Company</h1>
  </div>
  <div class="flex flex-row items-center justify-center p-5 border-b-2 border-t-2 border-white">
    <label class="italic">This is the app to give you quote of the day</label>
  </div>
  <div class="flex flex-row items-center justify-center w-full">
    <button
        @click="handleOnClick"
      class="p-5 border border-white rounded-xl font-bold w-1/4"
    >Generate Quote</button>
  </div>
</div>
</template>
