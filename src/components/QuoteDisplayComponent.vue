<script setup lang="ts">
import {computed} from "vue";

let {quote} = defineProps<{ quote: { quote: string } | null }>();

let localVal = computed(() => quote);
</script>

<template>
  <div class="flex-col flex w-full h-screen items-center justify-center">
    <div class="bg-white opacity-50 w-1/2 h-full rounded-xl text-center flex flex-row items-start justify-center p-5">
      <label class="text-4xl italic" v-if="localVal">
        "{{localVal?.quote}}"
      </label>
    </div>
  </div>
</template>
