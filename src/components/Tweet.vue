<script setup lang="ts">
import { ref } from "vue";
const tweets = ref([
  { id: 0, description: "Hello , world !" },
  { id: 1, description: "Second tweets" },
]);

const inputtingDescription = ref<string>("");
/**
 * InputBoxに入力された内容をTweetListに追加する
 */
const postTweet = () => {
  const ids = tweets.value.map((tweet) => tweet.id);

  const tweet = {
    id: ids.length === 0 ? 1 : Math.max(...ids) + 1,
    description: inputtingDescription.value,
  };
  inputtingDescription.value = "";
  console.log("post tweet", ids, tweet);
  tweets.value.push(tweet);
};

/**
 * Tweetを削除する
 * @param id 削除対象ID
 */
const deleteTweet = (id: number) => {
  tweets.value = tweets.value.filter((tweet) => tweet.id !== id);
};
</script>

<template>
  <div class="container">
    <h1>Tweeter</h1>
    <div class="form-container">
      <input v-model="inputtingDescription" class="tweet-input" />
      <button class="save-button" @click="postTweet">POST</button>
    </div>
    <div class="tweet-container">
      <p v-if="tweets.length <= 0">No tweets have been added</p>
      <ul>
        <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
          <span>{{ tweet.description }}</span>
          <button class="delete-button" @click="deleteTweet(tweet.id)">
            DELETE
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 1200px;
}

.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: slategray;
  padding: 24px 0;
  width: 60%;
  margin-bottom: 12px;
  border-radius: 4px;
}

.tweet-input {
  margin-bottom: 4px;
}

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

.save-button {
  color: aliceblue;
  font-weight: bold;
  background-color: aquamarine;
  border-radius: 2px;
  border: none;
  width: 60px;
  height: 25px;
  padding: 0;
}
.save-button:hover {
  background-color: aqua;
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
