<script setup lang="ts">
import { ref } from "vue";
import TweetPostForm from "./TweetPostForm.vue";
import TweetList from "./TweetList.vue";
const tweets = ref([
  { id: 0, description: "Hello , world !" },
  { id: 1, description: "Second tweets" },
]);

/**
 * InputBoxに入力された内容をTweetListに追加する
 */
const postTweet = (description: string) => {
  const ids = tweets.value.map((tweet) => tweet.id);

  const tweet = {
    id: ids.length === 0 ? 1 : Math.max(...ids) + 1,
    description: description,
  };
  console.log("post tweet", ids, tweet);
  tweets.value.push(tweet);
};

const deleteTweet = (id: number) => {
  tweets.value = tweets.value.filter((tweet) => tweet.id !== id);
};
</script>

<template>
  <div class="container">
    <h1>Tweeter</h1>
    <TweetPostForm @post-tweet="postTweet" />
    <div class="tweet-container">
      <p v-if="tweets.length <= 0">No tweets have been added</p>
      <ul>
        <TweetList :tweets="tweets" @delete-tweet="deleteTweet" />
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
</style>
