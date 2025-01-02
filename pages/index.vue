<template>
  <ConfettiEffect
    :ignition="ignitionConfetti"
    :eventX="clickedX"
    :eventY="clickedY"
  />

  <div class="statement-area">
    <TypingEffect
      v-if="questions"
      :text="currentQuestion.statement"
      :key="totalQuestions"
    />
  </div>
  <div class="options-area">
    <div>
      <component
        v-if="questions"
        :is="questionInfos[currentQuestion.category].component"
        :key="totalQuestions"
        :choices="currentQuestion.options"
        :orders="currentQuestion.options"
        @examineResult="examineResult"
      />
    </div>
  </div>
  <div class="control-area">
    <NextButton
      v-if="questions"
      :visible="
        !terminated &&
        answered &&
        totalQuestions + 1 != (route.query.q ?? questions.length)
      "
      @click="nextQuestion"
    />
  </div>
</template>

<script setup>
import TypingEffect from "~/components/TypingEffect.vue";
import ChoiceGroup from "~/components/ChoiceGroup.vue";
import OrderGroup from "~/components/OrderGroup.vue";
import qs from "~/questions.json";

const route = useRoute();

const questions = ref(null);
const currentQuestion = ref(null);

const correctedQuestions = ref(0);
const totalQuestions = ref(0);

const terminated = ref(false);
const answered = ref(false);

const ignitionConfetti = ref(false);
const clickedX = ref(0);
const clickedY = ref(0);

const questionInfos = ref({
  choice: {
    component: shallowRef(ChoiceGroup),
  },
  order: {
    component: shallowRef(OrderGroup),
  },
});

const nextQuestion = () => {
  totalQuestions.value++;
  currentQuestion.value = questions.value[totalQuestions.value];
  answered.value = false;
};

const examineResult = (event, correct) => {
  if (correct) {
    correctedQuestions.value++;

    ignitionConfetti.value = !ignitionConfetti.value;
    clickedX.value = event.clientX;
    clickedY.value = event.clientY;
  }

  if (questions.value.length == totalQuestions.value) {
    terminated.value = true;
  }
  answered.value = true;
};

onMounted(async () => {
  await $fetch("http://localhost:2434/questions", {})
    .then((res) => {
      questions.value = getShuffledQuestions(res);
      currentQuestion.value = questions.value[0];
    })
    .catch(() => {
      questions.value = getShuffledQuestions(qs);
      currentQuestion.value = questions.value[0];
    });
});
</script>

<style scoped>
.statement-area {
  height: 18%;
  text-align: center;
}

.options-area {
}

.control-area {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
