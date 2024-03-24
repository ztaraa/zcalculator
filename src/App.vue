<script setup lang="ts">
import CalculatorButton from './components/CalculatorButton.vue';
import CalculatorScreen from './components/CalculatorScreen.vue';
</script>

<template>
  <div class="flex flex-col gap-8 items-center justify-center my-5">
    <h1 class="text-4xl font-bold text-blue-950">zCalculator</h1>
    <div class="flex gap-3">
      <div class="bg-sky-950 w-fit h-[22rem] px-8 py-5 pt-12 rounded-xl flex flex-col items-end gap-3">
        <div class="flex gap-2 w-max">
          <CalculatorScreen :value="value" />
          <CalculatorButton :action="clearValue" text="⌫" />
        </div>
        <div class="grid grid-cols-4 grid-rows-4 gap-2">
          <CalculatorButton :action="updateValue(1)" text="1" />
          <CalculatorButton :action="updateValue(2)" text="2" />
          <CalculatorButton :action="updateValue(3)" text="3" />
          <CalculatorButton :action="updateValue('+')" text="+" />
          <CalculatorButton :action="updateValue(4)" class="row-start-2" text="4" />
          <CalculatorButton :action="updateValue(5)" class="row-start-2" text="5" />
          <CalculatorButton :action="updateValue(6)" class="row-start-2" text="6" />
          <CalculatorButton :action="updateValue('-')" class="row-start-2" text="-" />
          <CalculatorButton :action="updateValue(7)" class="row-start-3" text="7" />
          <CalculatorButton :action="updateValue(8)" class="row-start-3" text="8" />
          <CalculatorButton :action="updateValue(9)" class="row-start-3" text="9" />
          <CalculatorButton :action="updateValue('×')" class="row-start-3" text="×" />
          <CalculatorButton :action="updateValue('.')" class="row-start-4" text="." />
          <CalculatorButton :action="updateValue('0')" class="row-start-4" text="0" />
          <CalculatorButton :action="calc" class="row-start-4" text="=" />
          <CalculatorButton :action="updateValue('/')" class="row-start-4" text="÷" />
        </div>
      </div>
      <div class="bg-gray-300 px-4 py-4 rounded-xl flex flex-col justify-between gap-4 place-items-center h-[22rem] w-52">
        <h3 class="text-center text-xl font-bold uppercase mt-4">History</h3>
        <div class="h-48 px-4 overflow-scroll">
          <div class="flex flex-col gap-2">
            <div v-for="(item, index) in history" :key="index" title="Click to delete from history" @click="() => history.splice(index, 1)" class="text-right cursor-pointer rounded-md py-1 px-1 w-full hover:bg-black/10">
              {{ item }}
            </div>
          </div>
        </div>
        <CalculatorButton class="h-min" :action="clearHistory" text="Clear"/>
      </div>
    </div>
    <span class="text-gray-700">Made by <a class="text-sky-400 hover:text-sky-600 transition-colors" href="https://github.com/ztaraa">@ztaraa</a></span>
  </div>
</template>

<script lang="ts">
export default {
  data: () => {
    return {
      value: '',
      history: [] as string[]
    }
  },
  methods: {
    updateValue(newValue: any) {
      return () => {
        this.value += String(newValue)
      }
    },
    deleteLastDigit() {
      this.value = this.value.slice(0, -1);
    },
    clearValue() {
      this.value = ""
    },
    clearHistory() {
      this.history = []
    },
    calc() {
      let operation = this.value
      const val = this.value.replace('×', '*').replace('÷', '/');
      try {
        const result = eval(val) || "";
        this.value = String(result);
        result != "" && this.history.push(operation + "=" + this.value);
      } catch (error) {
        console.error('Error occurred during calculation:', error);
      }
    }
  }
}
</script>