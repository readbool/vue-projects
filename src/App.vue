<script setup lang="ts">
import QuoteGeneratorComponent from "./components/QuoteGeneratorComponent.vue";
import QuoteDisplayComponent from "./components/QuoteDisplayComponent.vue";
import {ref} from "vue";

let selectedQuote = ref(null);

const handleGetQuote = (quote: any) => {
  console.log(quote)
  selectedQuote.value = quote;
}

</script>

<template>
  <div class="flex flex-col h-full w-full bg-green-500 bg-gradient-to-tr from-green-500 to-cyan-500">
    <div class="flex flex-col mx-10">
      <div class="flex flex-row">
        <QuoteGeneratorComponent @handleGetQuote="handleGetQuote"/>
      </div>
      <div class="flex flex-row">
        <QuoteDisplayComponent :quote="selectedQuote" />
      </div>
    </div>
  </div>
</template>
