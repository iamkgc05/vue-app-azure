<script setup>

const props = defineProps({
    value : {
        type: [Number, String]
    }
});

const emit = defineEmits(['send-value']);

const handleClick = () => {
    emit('send-value', props.value)
};
</script>

<template>
    <button class="boutton" @click="handleClick">
        {{ value }}
    </button>
</template>

<style scoped>
.boutton {
  flex: 1;
  padding: 15px;
  font-size: 1.2rem;
  border: none;
  border-radius: 5px;
  background-color: white;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.boutton:hover {
  background-color: #e8e8e8;
  transform: translateY(-1px);
}

.boutton:active {
  transform: translateY(1px);
}
</style>