<template>
  <div>
    <h1>ファイル名一括変換アプリ</h1>
    <textarea
      v-model="inputText"
      placeholder="ファイル名を改行で入力"
      rows="5"
      cols="30"
    ></textarea>
    <button @click="convertFileNames">ファイル名を変換</button>
    <div v-if="message">{{ message }}</div>
    <div v-if="newFileNames.length">
      <h2>新しいファイル名:</h2>
      <ul>
        <li v-for="(name, index) in newFileNames" :key="index">{{ name }}</li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const inputText = ref("");
const message = ref("");
const newFileNames = ref<string[]>([]);

const formatFileName = (text: string): string => {
  return text.toLowerCase().replace(/\s+/g, "-");
};

const convertFileNames = () => {
  if (!inputText.value) {
    message.value = "ファイル名を入力してください。";
    return;
  }

  // 改行で分割して新しいファイル名を生成
  newFileNames.value = inputText.value.split("\n").map(formatFileName);
  message.value = "新しいファイル名を生成しました！";
};
</script>

<style scoped>
/* スタイルをここに追加 */
</style>
