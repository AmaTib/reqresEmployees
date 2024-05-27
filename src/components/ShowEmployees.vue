<script setup lang="ts">
import axios from "axios";
import { onMounted, ref } from "vue";
import { IEmployeeResponse } from "../models/IEmployeeResponse";
import { IEmployee } from "../models/IEmployee";

const employees = ref<IEmployee[]>([]);

async function getEmployees(): Promise<IEmployee[]> {
  const employeeResponse = await axios.get<IEmployeeResponse>(
    "https://reqres.in/api/users"
  );
  return employeeResponse.data.data;
}

onMounted(async () => {
  employees.value = await getEmployees();
});
</script>

<template>
  <section>
    <h1>Anställda</h1>
    <ul>
      <li v-for="employee in employees">
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
  width: 90%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

ul {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
  gap: 3em;

  li {
    width: 315px;
    list-style: none;
    display: flex;
    justify-content: flex-start;
    gap: 2em;
  }
}

img {
  border-radius: 50%;
  height: 6.5em;
}

a,
p {
  margin: 0;
  color: rgb(209, 209, 155);
}

@media only screen and (min-width: 600px) {
  ul {
    justify-content: center;
    gap: 5em;
  }
}
</style>
