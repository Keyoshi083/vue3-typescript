<script setup lang="ts">
import { Person } from "./Persons.vue";
type Props = {
  persons: Person[];
};

defineProps<Props>();

const emit = defineEmits(["delete"]);
const deletePerson = (id: number) => {
  emit("delete", id);
};
</script>

<template>
  <li v-for="person in persons" :key="person.id" class="person-list">
    <span>Name : {{ person.name }}</span>
    <span>Age : {{ person.age }}</span>
    <button class="delete-button" @click="deletePerson(person.id)">
      DELETE
    </button>
  </li>
</template>

<style scoped>
.person-list {
  list-style: none;
  background-color: darkgreen;
  margin-bottom: 12px;
  border-radius: 4px;
  font-size: 14px;
  display: flex;
  justify-content: space-between;
  padding: 8px, 20px;
  width: 300px;
}
</style>
