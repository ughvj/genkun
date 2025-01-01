<template>
  <ConfettiEffect
    :ignition="ignitionConfetti"
    :eventX="clickedX"
    :eventY="clickedY"
  />

  <div class="statement-area">
    <TypingEffect
      :text="currentQuestion.statement"
      :key="currentQuestionIndex"
    />
  </div>
  <div class="options-area">
    <div>
      <component
        :is="questionInfos[currentQuestion.category].component"
        :key="currentQuestionIndex"
        :choices="currentQuestion.options"
        :orders="currentQuestion.options"
        @examineResult="examineResult"
      />
    </div>
  </div>
  <div class="control-area">
    <NextButton :visible="terminated" @click="nextQuestion" />
  </div>
</template>

<script setup>
import TypingEffect from "~/components/TypingEffect.vue";
import ChoiceGroup from "~/components/ChoiceGroup.vue";
import OrderGroup from "~/components/OrderGroup.vue";
import questions from "~/questions.json";

const { data } = await useFetch("http://localhost:2434/questions");

const currentQuestionIndex = ref(0);
const currentQuestion = ref(questions[0]);

const correctedQuestions = ref(0);
const totalQuestions = ref(1);
const terminated = ref(false);

const nextQuestion = () => {
  currentQuestionIndex.value++;
  totalQuestions.value++;
  currentQuestion.value = data.value[currentQuestionIndex.value];
  terminated.value = false;
};

const ignitionConfetti = ref(false);
const clickedX = ref(0);
const clickedY = ref(0);

const examineResult = (event, correct) => {
  console.log(data.value[0].statement);
  if (correct) {
    correctedQuestions.value++;

    ignitionConfetti.value = !ignitionConfetti.value;
    clickedX.value = event.clientX;
    clickedY.value = event.clientY;
  }
  terminated.value = true;
};

const questionInfos = ref({
  choice: {
    component: ChoiceGroup,
  },
  order: {
    component: OrderGroup,
  },
});
</script>

<style scoped>
.statement-area {
  height: 18%;
  text-align: center;
}

.options-area {
  height: 70%;
}

.control-area {
  height: 12%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
