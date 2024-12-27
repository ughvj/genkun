<template>
  <form method="post" action="http://localhost:2434/genkun">
    <p>元勲の名前(漢字 空白なし)</p>
    <p>
      <input
        type="text"
        name="genkun_name_kanji"
        placeholder="登録したい元勲の名前を入力"
        required
      />
    </p>

    <p>元勲の名前(ひらがな 空白なし)</p>
    <p>
      <input
        type="text"
        name="genkun_name_hiragana"
        placeholder="登録したい元勲の名前を入力"
        required
      />
    </p>

    <p>画像ファイル名</p>
    <p>
      <input
        type="text"
        name="genkun_src"
        placeholder="元勲の画像ファイル名を入力(拡張子含)"
        required
      />
    </p>
    <p><button type="submit">登録</button></p>
  </form>
</template>
