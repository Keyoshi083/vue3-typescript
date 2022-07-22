<script setup lang="ts">
import { ref } from "vue";
import PersonPostForm from "./PersonPostForm.vue";
import PersonList from "./PersonList.vue";
export type Person = {
  id: number;
  name: string;
  age: number;
};
const persons = ref<Person[]>([
  {
    id: 1,
    name: "Mizuki",
    age: 29,
  },
  {
    id: 2,
    name: "Ruri",
    age: 30,
  },
]);

const registerPerson = (person: Person) => {
  persons.value.push(person);
};

const deletePerson = (id: number) => {
  persons.value = persons.value.filter((person) => person.id !== id);
};
</script>

<template>
  <h1>Title</h1>
  <div class="container">
    <PersonPostForm @register="registerPerson" />
    <div class="list-container">
      <ul>
        <PersonList :persons="persons" @delete="deletePerson" />
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

template {
  width: 1000px;
}
</style>
