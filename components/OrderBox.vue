<template>
  <div class="order-box" @click="onClick($event)">
    <slot></slot>
  </div>
</template>

<script setup>
const props = defineProps({
  index: {
    type: Number,
    required: true,
  },
});

const emit = defineEmits();

const onClick = (event) => {
  emit("select", event, props.index);
};
</script>

<style scoped>
.order-box {
  display: flex;
  justify-content: center;
  width: 50%;
}

@media (min-width: 1200px) {
  .order-box {
    width: fit-content;
  }
}
</style>
