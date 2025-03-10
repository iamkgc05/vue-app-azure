<script setup>
import { ref } from 'vue';
import Ecran from './components/Ecran.vue';
import BoutonCalculatrice from './components/BoutonCalculatrice.vue';


const leftOperator = ref("");
const rightOperator = ref("");
const operation = ref(' ');
const result = ref(0);
const isFirstNumber = ref(true);
const bouttons_char = [['+', '-', '='], ['/', '*', 'C']];
const bouttons = [[0, 1, 2], [3, 4, 5], [6, 7, 8], [9]];
const handleButtonClick = (value) => {
  if (typeof value === 'number') {
    if (result.value === 1) {
      leftOperator.value = value;
      rightOperator.value = "";
      operation.value = ' ';
      result.value = 0;
      isFirstNumber.value = true;
    } else {
      if (isFirstNumber.value) {
        leftOperator.value = leftOperator.value * 10 + value;
      } else {
        rightOperator.value = rightOperator.value * 10 + value;
      }
    }
  } else if (['+', '-', '*', '/'].includes(value)) {
    operation.value = value;
    isFirstNumber.value = false;
  } else if (value === 'C') {
    leftOperator.value = "";
    rightOperator.value = "";
    operation.value = ' ';
    result.value = 0;
    isFirstNumber.value = true;
  } else if (value === '=') {
    result.value = 1;
  }
};
</script>

<template>
  <h1>Bonjour La team</h1>
  <div class="calculator">
    <div class="ecran">
      <Ecran :leftOperator="leftOperator" :operation="operation" :rightOperator="rightOperator" :result="result" />
    </div>
    <div class="grid">
      <div v-for="(row, rowIndex) in bouttons_char" :key="'char' + rowIndex" class="row">
        <BoutonCalculatrice v-for="(valeur, colIndex) in row" :key="'char' + rowIndex + colIndex" :value="valeur"
          @click="handleButtonClick(valeur)" />
      </div>
      <div v-for="(row, rowIndex) in bouttons" :key="'num' + rowIndex" class="row">
        <BoutonCalculatrice v-for="(valeur, colIndex) in row" :key="'num' + rowIndex + colIndex" :value="valeur"
          @click="handleButtonClick(valeur)" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.calculator {
  max-width: 300px;
  margin: 20px auto;
  padding: 15px;
  background-color: #f0f0f0;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.ecran {
  margin-bottom: 15px;
  width: 100%;
}

.grid {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.row {
  display: flex;
  gap: 10px;
}
</style>
