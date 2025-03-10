<script setup>
import { computed } from 'vue';
const props = defineProps({
    leftOperator : {
        type: [Number, String],
        required: true,
        default: ""
    },
    operation : {
        type: String,
        required: true,
        default: ' '
    },
    rightOperator : {
        type: [Number, String],
        required: true,
        default: ""
    },
    result : Number
})

const realiserCalcul = computed(() => {
    if (props.result === 1) {
        switch(props.operation) {
            case '+':
                return props.leftOperator + props.rightOperator;
            case '-':
                return props.leftOperator - props.rightOperator;
            case '*':
                return props.leftOperator * props.rightOperator;
            case '/':
                return props.rightOperator !== 0 ? props.leftOperator / props.rightOperator : 'Error';
            default:
                return 0;
        }
    }
    return '';
})


const affichageCalcul = computed(() => {
    return `${props.leftOperator} ${props.operation} ${props.rightOperator}`;
})

</script>

<template>
    <div class="ecran1">
        {{ affichageCalcul }}
        <span v-if="props.result === 1"> = </span>
        
    </div>
    <div class="ecran2">
        <span v-if="props.result === 1"> {{ realiserCalcul }}</span>
    </div>
</template>

<style scoped>
.ecran1, .ecran2 {
  background-color: white;
  padding: 10px 15px;
  text-align: right;
  font-size: 1.5rem;
  border-radius: 5px;
  margin-bottom: 5px;
  min-height: 2rem;
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
  color: #000000;
}
</style>