<script lang="ts" setup>
import {ref} from "vue";

const calcButtons = [
    '7',
    '8',
    '9',
    '/',
    '4',
    '5',
    '6',
    '*',
    '1',
    '2',
    '3',
    '-',
    '0',
    '.',
    '=',
    '+',
];

let calcVal:string = ref('0');

let operationResult = ref(0);

const handleBtnClick = (btnValue: string) => {
  let operations = [
      '+','/','*','-'
  ];

  if (calcVal.value === '0') {
    calcVal.value = '';
  }

  let lastEntry = calcVal.value.slice(-1);

  if (isNaN(lastEntry) && operations.includes(btnValue)) {
    return;
  }

  if (isNaN(lastEntry) && btnValue === '.') {
    return;
  }

  if (btnValue === '=') {
    let toProcessString = calcVal.value;

    let indexToWithOperations = [];

    let marker = 0;

    for (let i = 0; i < toProcessString.length; i++) {
      if (operations.includes(toProcessString.charAt(i))) {
        indexToWithOperations.push(toProcessString.slice(marker, i));
        marker = i + 1;
        indexToWithOperations.push(toProcessString.charAt(i));
      }

      if (i+1 === toProcessString.length) {
        indexToWithOperations.push(toProcessString.slice(marker, i+1));
      }
    }

    let numberToOperate = 0;

    for (let x = 0; x < indexToWithOperations.length; x++) {
        if (indexToWithOperations[x + 1] === 'undefined') {
          return;
        }

        if (!isNaN(indexToWithOperations[x])) {
          if (indexToWithOperations[x + 1] === '+') {
            numberToOperate += parseFloat(indexToWithOperations[x]);
          }

          if (indexToWithOperations[x + 1] === '-') {
            numberToOperate -= parseFloat(indexToWithOperations[x]);
          }

          if (indexToWithOperations[x + 1] === '*') {
            numberToOperate *= parseFloat(indexToWithOperations[x]);
          }

          if (indexToWithOperations[x + 1] === '/') {
            numberToOperate /= parseFloat(indexToWithOperations[x]);
          }
        }
    }

    calcVal.value = numberToOperate;

    return;
  }

  calcVal.value = calcVal.value + btnValue;
}

const handleClear = () => {
  calcVal.value = '0';
}

</script>

<template>
  <div class="h-[600px] w-[700px] border border-slate-400 rounded flex flex-col gap-10 p-5">
    <input
        :value="calcVal"
        class="h-[50px] w-full border border-slate-400 rounded p-1 text-[16px]"
        disabled
    />
    <div class="grid grid-cols-4 gap-3" >
      <button
          v-for="buttonItem in calcButtons" class="bg-slate-400 p-5 rounded"
          @click="handleBtnClick(buttonItem)"
      >{{buttonItem}}</button>
    </div>
    <div class="flex flex-row w-full items-center justify-center">
      <button  class="bg-slate-400 p-5 w-full rounded" @click="handleClear">
        C
      </button>
    </div>
  </div>
</template>
