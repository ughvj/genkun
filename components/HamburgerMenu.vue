<template>
  <div>
    <img
      src="/abstracts/hamburger.png"
      @click="toggleMenu"
      class="hamburger-icon"
    />

    <nav :class="{ open: isOpen }" class="side-menu">
      <div class="symbol-container">
        <img src="/logo.jpg" />
        <div class="close-area" @click="toggleMenu">
          <div class="close-button"></div>
        </div>
      </div>
      <ul>
        <li><a href="/?q=10">10問</a></li>
        <li><a href="/?q=30">30問</a></li>
        <li><a href="/?q=50">50問 </a></li>
      </ul>
    </nav>
  </div>
</template>

<script setup>
import { ref } from "vue";

const isOpen = ref(false);

const toggleMenu = () => {
  isOpen.value = !isOpen.value;
};
</script>

<style scoped>
.hamburger-icon {
  width: 50px;
  height: 50px;
  padding-right: 20px;
}
.side-menu {
  position: fixed;
  top: 0;
  left: -100%; /* メニューを左側に隠す */
  width: fit-content;
  min-width: 17vw;
  height: 100%;
  background-color: #fff;
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.2);
  transition: left 0.3s ease; /* アニメーションでスライド */
  z-index: 5;
}

.side-menu.open {
  left: 0; /* メニューが開いたときに表示 */
}

.side-menu ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.side-menu li {
  padding: 20px;
  text-align: center;
  border-bottom: 1px solid #eee;
}

.side-menu li a {
  text-decoration: none;
  color: #333;
  display: block;
}

.symbol-container {
  display: flex; /* フレックスボックスでレイアウト */
  align-items: center; /* 縦方向に中央揃え */
  justify-content: space-between; /* 左右に要素を配置 */
}

.symbol-container img {
  max-height: 30px;
  margin-top: 6px;
  margin-left: 6px;
  margin-right: 6px;
}

.close-area {
  display: flex; /* フレックスボックスでレイアウト */
  align-items: center; /* 縦方向に中央揃え */
  width: 30px;
  height: 30px;
  cursor: pointer;
  margin-top: 10px;
  margin-right: 10px;
}

.close-button {
  width: 100%;
  height: 10%;
  position: relative;
}

.close-button::before,
.close-button::after {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  width: 20px;
  height: 2px;
  background-color: black;
  border-radius: 2px;
  transform-origin: center;
  transform: translate(-50%, -50%) rotate(45deg);
}

.close-button::after {
  transform: translate(-50%, -50%) rotate(-45deg);
}
</style>
