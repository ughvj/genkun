<template>
  <p>元勲の名前(漢字 空白なし)</p>
  <p>
    <input
      type="text"
      v-model="genkunNameKanji"
      placeholder="登録したい元勲の名前を入力"
      required
    />
  </p>

  <p>元勲の名前(ひらがな 空白なし)</p>
  <p>
    <input
      type="text"
      v-model="genkunNameHiragana"
      placeholder="登録したい元勲の名前を入力"
      required
    />
  </p>

  <p>画像ファイル名</p>
  <p>
    <input
      type="text"
      v-model="genkunSrc"
      placeholder="元勲の画像ファイル名を入力(拡張子含)"
      required
    />
  </p>
  <p><button @click="register">登録</button></p>
  <AdminInformationMessage :text="message" />
</template>

<script setup>
const genkunNameKanji = ref("");
const genkunNameHiragana = ref("");
const genkunSrc = ref("");
const message = ref("");

const register = async () => {
  await $fetch("http://localhost:2434/genkun", {
    method: "POST",
    body: {
      name_kanji: genkunNameKanji.value,
      name_yomi_hiragana: genkunNameHiragana.value,
      src: genkunSrc.value,
    },
    headers: {
      "Content-Type": "application/json",
    },
  }).then((res) => {
    message.value = res.message;
  });
};
</script>

<style scoped></style>
