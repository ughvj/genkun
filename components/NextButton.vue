<template>
  <button class="soft-button" @click="onClick">次へ</button>
</template>

<script setup>
const emit = defineEmits();

const onClick = () => {
  emit("nextQuestion");
};
</script>

<style scoped>
/* ボタンのスタイル */
.soft-button {
  background-color: #f4f8ff; /* 優しい青系の背景色 */
  color: #3b5998; /* テキストの落ち着いた色 */
  border: 3px solid black; /* 枠線をなくす */
  border-radius: 12px; /* 丸みをつける */
  padding: 10px 20px; /* ボタン内の余白 */
  font-size: 16px; /* 適度なフォントサイズ */
  font-weight: 500; /* やや太めの文字 */
  font-family: monospace;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* 軽い影で立体感を追加 */
  cursor: pointer; /* ポインタカーソルを表示 */
  transition: background-color 0.3s, transform 0.2s, box-shadow 0.3s; /* ホバー時のアニメーション */
}

/* ホバー時のスタイル */
.soft-button:hover {
  background-color: #e0edff; /* 少し濃い背景色 */
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15); /* 影を強調 */
  transform: translateY(-2px); /* 軽く浮く演出 */
}

/* アクティブ（クリック時）のスタイル */
.soft-button:active {
  background-color: #d4e5ff; /* さらに濃い背景色 */
  transform: translateY(0); /* 押し込まれるように */
  box-shadow: 0 3px 5px rgba(0, 0, 0, 0.1); /* 影を縮小 */
}
</style>
