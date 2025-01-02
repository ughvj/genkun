<template>
  <div class="image-container" @click="onClick($event)">
    <img :src="src" class="image" />
    <p class="image-caption">{{ caption }}</p>
    <img v-if="overlay === '1'" src="/abstracts/_1g.png" class="overlay" />
    <img v-if="overlay === '2'" src="/abstracts/_2g.png" class="overlay" />
    <img v-if="overlay === '3'" src="/abstracts/_3g.png" class="overlay" />
    <img v-if="overlay === '4'" src="/abstracts/_4g.png" class="overlay" />
    <img v-if="overlay === 'o'" src="/abstracts/o.png" class="overlay" />
    <img v-if="overlay === 'x'" src="/abstracts/x.png" class="overlay" />
    <img
      v-if="overlay_ans === '1'"
      src="/abstracts/_1r.png"
      class="overlay_ans"
    />
    <img
      v-if="overlay_ans === '2'"
      src="/abstracts/_2r.png"
      class="overlay_ans"
    />
    <img
      v-if="overlay_ans === '3'"
      src="/abstracts/_3r.png"
      class="overlay_ans"
    />
    <img
      v-if="overlay_ans === '4'"
      src="/abstracts/_4r.png"
      class="overlay_ans"
    />
  </div>
</template>

<script setup>
const props = defineProps({
  src: {
    type: String,
    required: true,
  },
  caption: {
    type: String,
    required: true,
  },
  overlay: {
    type: String,
    default: "none",
  },
  overlay_ans: {
    type: String,
    default: "none",
  },
});

const emit = defineEmits();

const onClick = (event) => {
  emit("onClick", event);
};
</script>

<style scoped>
.image-container {
  width: 80%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.image {
  width: 60%;
  height: auto;
  object-fit: contain;
}

.image-caption {
  margin-top: 10px;
  font-size: 16px;
  color: #333;
  text-align: center;
  font-size: 1.2rem;
}

.overlay {
  position: absolute;
  height: auto;
  object-fit: contain;
  opacity: 0.5;
  width: 50%;
}

.overlay_ans {
  position: absolute;
  height: auto;
  object-fit: contain;
  opacity: 0.7;
  width: 50%;
}

@media (min-width: 1200px) {
  .image {
    width: 100%;
  }

  .overlay {
    width: fit-content;
  }

  .overlay_ans {
    width: fit-content;
  }

  .image:hover {
    transform: translateY(-10px); /* 上に10px浮かせる */
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2); /* 影をつけて浮いているように見せる */
  }
}
</style>
