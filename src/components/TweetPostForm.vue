<script setup lang="ts">
import { ref, defineEmits } from "vue";
const inputtingDescription = ref<string>("");

const postTweet = () => {
  emit("post-tweet", inputtingDescription.value);
};

const emit = defineEmits(["post-tweet"]);
</script>
<template>
  <div class="form-container">
    <input v-model="inputtingDescription" class="tweet-input" />
    <button class="save-button" @click="postTweet">POST</button>
  </div>
</template>

<style scoped>
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
  margin-bottom: 8px;
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
</style>
