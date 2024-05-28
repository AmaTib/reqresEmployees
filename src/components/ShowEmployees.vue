<script setup lang="ts">
import { IEmployee } from "../models/IEmployee";

export interface IEmployeeProps {
  employees: IEmployee[];
}

defineProps<IEmployeeProps>();
</script>

<template>
  <section>
    <h1>Anställda</h1>
    <ul>
      <li v-for="employee in employees" :key="employee.id">
        <img :src="employee.avatar" alt="employee img" />
        <div>
          <h3>{{ employee.first_name }} {{ employee.last_name }}</h3>
          <p>Email:</p>
          <a :href="'mailto:' + employee.email">{{ employee.email }}</a>
        </div>
      </li>
    </ul>
  </section>
</template>

<style scoped>
h1 {
  font-size: 2em;
}

section {
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
  padding-left: 0;
  gap: 3em;
  width: min-content;

  li {
    width: 325px;
    list-style: none;
    display: flex;
    justify-content: flex-start;
    gap: 2em;
  }
}

img {
  border-radius: 50%;
  height: 6.5em;
  width: 6.5em;

  border: 10px solid rgb(215, 215, 198);
}

a,
p {
  margin: 0;
  color: rgb(209, 209, 155);
}

@media only screen and (min-width: 600px) {
  ul {
    justify-content: center;
    width: 90%;
    gap: 4em;
  }
}
</style>
