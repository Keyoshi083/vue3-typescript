<script setup lang="ts">
import { defineProps } from "vue";
type Tweet = {
  id: number;
  description: string;
};
//Propsに対して関数を渡すと言う方法がある（Reactではこちらが一般的）
type Props = {
  tweets: Tweet[];
  // deleteTweet: (id: number) => void;
};

//definePropsで親コンポからプロパティを受け取るようにする
//受け取るPropsについては型定義をしておく
defineProps<Props>();

/**
 * Vue.jsの公式は以下のようにemitを用いることを推奨。
 */
const emit = defineEmits(["delete-tweet"]);
const deleteTweet = (id: number) => {
  emit("delete-tweet", id);
};
</script>

<template>
  <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
    <span>{{ tweet.description }}</span>
    <button class="delete-button" @click="deleteTweet(tweet.id)">DELETE</button>
  </li>
</template>

<style scoped>
.tweet-list {
  list-style: none;
  margin-bottom: 12px;
  padding: 8px, 20px;
  width: 300px;
  height: 30px;
  border-radius: 4px;
  font-size: 14px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: steelblue;
}

.delete-button {
  color: aliceblue;
  font-weight: bold;
  background-color: indianred;
  border-radius: 2px;
  border: none;
  width: 60px;
  height: 25px;
  padding: 0;
  margin-right: 8px;
}

.delete-button:hover {
  background-color: coral;
}
</style>
