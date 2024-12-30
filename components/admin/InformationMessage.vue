<!-- template -->
<template>
  <div class="information-message">
    <span>{{ displayedText }}</span>
  </div>
</template>

<!-- script -->
<script setup>
const props = defineProps({
  text: {
    type: String, // 文字列型
    required: true, // 必須
  },
});

const displayedText = ref(""); // 表示される文字列

watch(
  () => props.text,
  (newValue) => {
    displayedText.value = newValue;
  }
);

// タイピングエフェクトのロジック
const startTyping = (index) => {
  const type = () => {
    if (index < props.text.length) {
      displayedText.value += props.text[index];
      index++;
      setTimeout(type, props.typingSpeed);
    }
  };

  type();
};
</script>

<!-- style -->
<style scoped></style>
