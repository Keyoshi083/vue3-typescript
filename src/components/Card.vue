<script setup lang="ts">
import { defineProps } from "vue";
defineProps<{
  title: string;
}>();
</script>

<template>
  <div class="card-container">
    <span class="title">{{ title }}</span>
    <!-- 親コンポの内部で指定されたものを表示する（slot) -->
    <slot></slot>
  </div>
  <div class="footer">
    <slot name="footer"><span>Default Footer</span></slot>
  </div>
</template>

<style scoped>
.card-container {
  box-shadow: 2, 8px, black;
  border-radius: 8px 8px 0px 0px;
  padding: 20px 20px;
  width: 300px;
  height: 80px;
  background-color: #ccc;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.title {
  font-size: 20px;
  font-weight: 600;
}

.footer {
  display: flex;
  height: 30px;
  background-color: aquamarine;
  width: 100%;
  border-radius: 0px 0px 8px 8px;
  justify-content: center;
  align-items: center;
}
</style>
