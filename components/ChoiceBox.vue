<template>
  <div class="choice-box" @click="onClick">
    <slot></slot>
  </div>
</template>

<script setup>
const props = defineProps({
  correct: {
    type: Boolean,
    required: true,
  },
});

const emit = defineEmits();

const onClick = (event) => {
  if (props.correct) {
    emit("terminate", event, true);
  } else {
    emit("terminate", event, false);
  }
};
</script>

<style scoped>
.choice-box {
  display: flex;
  justify-content: center;
  width: 50%;
}

@media (min-width: 1025px) {
  .choice-box {
    width: fit-content;
  }
}
</style>
