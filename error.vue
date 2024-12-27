<template>
  {{ error.message }}
  <button @click="handleError">clear error</button>
</template>

<script setup>
const props = defineProps({
  error: Object,
});

const handleError = () => {
  clearError({
    redirect: "/",
  });
};
</script>
