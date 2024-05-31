<script setup lang="ts">
import { IEmployee } from "../models/IEmployee";

export interface IEmployeeProps {
  employees: IEmployee[];
}

defineProps<IEmployeeProps>();
</script>

<template>
  <section>
    <h2>Våra medarbetare</h2>
    <ul>
      <li v-for="employee in employees" :key="employee.id">
        <img :src="employee.avatar" alt="employee img" />
        <div>
          <h3>{{ employee.first_name }} {{ employee.last_name }}</h3>
          <a :href="'mailto:' + employee.email"
            >Maila {{ employee.first_name }}</a
          >
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
}

li {
  width: 315px;
  list-style: none;
  display: flex;
  justify-content: flex-start;
  gap: 2em;
}

img {
  border-radius: 50%;
  height: 6.5em;
  width: 6.5em;
  object-fit: cover;
  border: 10px solid rgb(215, 215, 198);
}

a,
p {
  margin: 0;
  color: rgb(209, 209, 155);
}

@media only screen and (min-width: 600px) {
  section {
    margin-bottom: 2em;
  }

  ul {
    justify-content: center;
    width: 90%;
    gap: 4em;
  }

  h2 {
    margin-bottom: 3em;
  }
}
</style>
