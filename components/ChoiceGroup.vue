<template>
  <div class="choice-group">
    <ChoiceBox
      v-for="(choice, index) in choices"
      :correct="choice.correct"
      @terminate="terminator"
    >
      <ImageDisplay
        :src="`${choice.src}`"
        :caption="choice.caption"
        :overlay="overlay(choice.correct)"
      />
    </ChoiceBox>
  </div>
</template>

<script setup>
import { ref } from "vue";
const props = defineProps({
  choices: {
    type: Array,
  },
});
const terminated = ref(false);
const emit = defineEmits();

const terminator = (event, correct) => {
  if (terminated.value) return;
  terminated.value = true;
  emit("examineResult", event, correct);
};

const overlay = (correct) => {
  if (terminated.value && correct) {
    return "o";
  }
  if (terminated.value && !correct) {
    return "x";
  }
  return "none";
};
</script>

<style scoped>
.choice-group {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
</style>
