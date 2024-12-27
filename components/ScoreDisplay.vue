<template>
  <span>{{ props.numerator }} / {{ props.denominator }}</span>
</template>

<script setup>
const props = defineProps({
  denominator: {
    type: Number,
    required: true,
  },
  numerator: {
    type: Number,
    required: true,
  },
});
</script>

<style scoped>
span {
  font-size: 1.5rem;
  color: #333;
}
</style>
