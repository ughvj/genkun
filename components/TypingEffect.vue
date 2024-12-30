<!-- template -->
<template>
  <div class="typing-effect">
    <span>{{ displayedText }}</span>
    <span class="cursor" :class="{ blinking: isCursorBlinking }">|</span>
  </div>
</template>

<!-- script -->
<script setup>
const props = defineProps({
  text: {
    type: String, // 文字列型
    required: true, // 必須
  },
  typingSpeed: {
    type: Number, // 数値型
    default: 50, // デフォルト値
  },
  cursorBlinkDuration: {
    type: Number, // 数値型
    default: 5000, // デフォルト値
  },
});

const displayedText = ref(""); // 表示される文字列
const isCursorBlinking = ref(true); // カーソルの点滅状態を管理

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

// カーソルの点滅を一定時間後に停止
const stopCursorBlinking = () => {
  setTimeout(() => {
    isCursorBlinking.value = false;
  }, props.cursorBlinkDuration);
};

onMounted(() => {
  startTyping(0);
  stopCursorBlinking();
});
</script>

<!-- style -->
<style scoped>
.typing-effect {
  width: 100%;
  font-family: monospace;
  font-size: 1.5rem;
  white-space: pre-wrap;
}

.cursor {
  display: inline-block;
  background-color: black;
  color: transparent;
  width: 8px;
  height: 1.5rem;
  margin-left: 2px;
}

.blinking {
  animation: blink 0.6s step-start infinite;
}

@keyframes blink {
  50% {
    background-color: transparent;
  }
}
</style>
