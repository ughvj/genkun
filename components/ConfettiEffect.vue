<template>
  <canvas ref="confettiCanvas" class="confetti-canvas"></canvas>
</template>

<script setup>
const props = defineProps({
  ignition: {
    type: Boolean,
    required: true,
  },
  eventX: {
    type: Number,
    required: true,
  },
  eventY: {
    type: Number,
    required: true,
  },
});

const confettiCanvas = ref(null);

const triggerConfetti = () => {
  const canvas = confettiCanvas.value;
  if (!canvas) return;

  const ctx = canvas.getContext("2d");
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  // クリック位置を取得
  const x = props.eventX;
  const y = props.eventY;

  // クラッカー（粒子）を生成
  const particles = [];
  for (let i = 0; i < 100; i++) {
    particles.push(createParticle(x, y));
  }

  // 粒子の動きをアニメーション
  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height); // 画面をクリア
    particles.forEach((particle, index) => {
      if (particle.alpha <= 0) {
        particles.splice(index, 1); // 透明度が0以下になったら削除
      } else {
        particle.update();
        particle.draw(ctx);
      }
    });

    if (particles.length > 0) {
      requestAnimationFrame(animate);
    }
  }

  // パーティクルの初期化
  function createParticle(x, y) {
    return {
      x: x, // クリックした位置
      y: y,
      radius: Math.random() * 5 + 5, // ランダムな大きさ
      color: getRandomColor(),
      speedX: Math.random() * 10 - 5, // ランダムなX方向のスピード
      speedY: Math.random() * 10 - 5, // ランダムなY方向のスピード
      alpha: 1, // 初期の透明度

      // 更新関数
      update() {
        this.x += this.speedX;
        this.y += this.speedY;
        this.alpha -= 0.02; // 徐々に透明に
      },

      // 描画関数
      draw(ctx) {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
        ctx.fillStyle = this.color;
        ctx.globalAlpha = this.alpha;
        ctx.fill();
      },
    };
  }

  // ランダムな色を生成
  function getRandomColor() {
    const letters = "0123456789ABCDEF";
    let color = "#";
    for (let i = 0; i < 6; i++) {
      color += letters[Math.floor(Math.random() * 16)];
    }
    return color;
  }

  animate(); // アニメーション開始
};

watch(
  () => props.ignition,
  () => {
    triggerConfetti();
  }
);
</script>

<style scoped>
.confetti-canvas {
  position: absolute;
  top: 0;
  left: 0;
  pointer-events: none; /* キャンバスがクリックを受けないようにする */
  z-index: 9999;
}
</style>
