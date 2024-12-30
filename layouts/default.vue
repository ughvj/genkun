<template>
  <header>
    <div class="logo-container">
      <HamburgerMenu />
      <img src="/logo.jpg" />
    </div>
  </header>

  <div class="main-container">
    <slot></slot>
  </div>
</template>

<style scoped>
.logo-container {
  position: fixed; /* ヘッダーを固定 */
  top: 0;
  left: 0;
  width: 100%; /* コンテナの幅を画面幅に合わせる */
  padding: 10px 20px; /* 上下・左右に適切な余白を設定 */
  background-color: #fff; /* 背景色 */
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); /* 軽い影を付ける */
  box-sizing: border-box; /* padding を幅に含む */
  display: flex; /* フレックスボックスでレイアウト */
  align-items: center; /* 縦方向に中央揃え */
  justify-content: left; /* 左右に要素を配置 */
  z-index: 1000; /* 前面に表示 */
  overflow: hidden; /* 子要素がはみ出さないようにする */
}
.logo-container img {
  max-height: 40px;
  margin-right: 8px;
}

.main-container {
  margin-top: 60px;
  padding: 10px;
  min-width: 90vw;
  min-height: 90vh;
}
</style>
