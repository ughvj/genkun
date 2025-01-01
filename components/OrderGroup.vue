<template>
  <div class="order-group">
    <OrderBox
      v-for="(order, index) in orders"
      :key="index"
      :index="index"
      @select="selector"
    >
      <ImageDisplay
        :src="`${order.src}`"
        :caption="order.caption"
        :overlay="String(states[index].currentOrder)"
        :overlay_ans="states[index].overlayAns"
      />
    </OrderBox>
  </div>
</template>

<script setup>
import { ref } from "vue";
const props = defineProps({
  orders: {
    type: Array,
  },
});
const states = ref(
  [...Array(4)].reduce((acc) => {
    return [
      ...acc,
      {
        selected: false,
        currentOrder: 0,
        overlayAns: "none",
      },
    ];
  }, [])
);
const terminated = ref(false);
const emit = defineEmits();

const selector = (event, index) => {
  if (terminated.value) return;
  const target = states.value[index];
  target.selected = !target.selected;
  if (target.selected) {
    // false -> true
    target.currentOrder =
      states.value.reduce((acc, cur) => {
        if (cur.currentOrder > acc) {
          return cur.currentOrder;
        }
        return acc;
      }, 0) + 1;
  } else {
    // true -> false
    states.value.forEach((e, idx) => {
      if (e.currentOrder > target.currentOrder) {
        states.value[idx].currentOrder--;
      }
    });
    target.currentOrder = 0;
  }
  // 全問チェック
  const selectedAll = states.value.reduce((acc, cur) => {
    if (!cur.selected) return false;
    return acc;
  }, true);

  if (selectedAll) {
    const correctAll = states.value.reduce((acc, cur, idx) => {
      if (props.orders[idx].correct !== cur.currentOrder) return false;
      return acc;
    }, true);
    if (!correctAll) {
      states.value.forEach((e, idx) => {
        if (props.orders[idx].correct === e.currentOrder) return;
        states.value[idx].overlayAns = String(props.orders[idx].correct);
      });
    }
    terminated.value = true;
    emit("examineResult", event, correctAll);
  }
};
</script>

<style scoped>
.order-group {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
</style>
