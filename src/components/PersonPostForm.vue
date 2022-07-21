<script setup lang="ts">
import { computed, ref } from "vue";

const inputtingName = ref<string>("");
const inputtingAge = ref<number | null>(null);

const emit = defineEmits(["register"]);
const register = () => {
  const person = {
    id: Math.random(),
    name: inputtingName.value,
    age: inputtingAge.value,
  };
  console.log(person);
  emit("register", person);
};

const inputNameBgColor = computed(() => (isValidName.value ? "field" : "Red"));
const inputNameLengthLimit = 15;

const isValidName = computed(
  () => inputtingName.value.length < inputNameLengthLimit
);
</script>

<template>
  <div class="form-container">
    <div class="input-container">
      <div class="input-column">
        <label>name:</label>
        <input class="input-name" v-model="inputtingName" />
      </div>
      <span class="error-message" v-if="!isValidName"
        >{{ inputNameLengthLimit }} characters or less , please.</span
      >
      <div class="input-column">
        <label>age:</label>
        <input class="input" v-model="inputtingAge" type="number" />
      </div>
    </div>
    <button disabled="true" class="register-button" @click="register">
      Register
    </button>
  </div>
</template>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: darkcyan;
  padding: 24px 0;
  width: 800px;
  margin-bottom: 12px;
  border-radius: 4px;
}

.input-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 50px;
  margin-bottom: 20px;
}

.input-column {
  width: 200px;
  display: flex;
  justify-content: space-between;
}

input {
  width: 120px;
  margin-bottom: 8px;
}

.input-name {
  background-color: v-bind(inputNameBgColor);
}

label {
  font-size: 14px;
  font-weight: bold;
}
</style>
