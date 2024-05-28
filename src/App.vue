<script setup lang="ts">
import { onMounted, ref } from "vue";
import { IEmployee } from "./models/IEmployee";
import { IEmployeeResponse } from "./models/IEmployeeResponse";
import axios from "axios";
import ShowEmployees from "./components/ShowEmployees.vue";
import PageNavigation from "./components/PageNavigation.vue";

const employees = ref<IEmployee[]>([]);
const currentPage = ref(1);

onMounted(async () => {
  employees.value = await getEmployees(currentPage.value);
});

async function getEmployees(pageNr: number): Promise<IEmployee[]> {
  const employeeResponse = await axios.get<IEmployeeResponse>(
    "https://reqres.in/api/users?page=" + pageNr
  );
  return employeeResponse.data.data;
}

async function changePage(pageNr: number) {
  employees.value = await getEmployees(pageNr);
  currentPage.value = pageNr;
}
</script>

<template>
  <ShowEmployees :employees="employees" />
  <PageNavigation :current-page="currentPage" @change-page="changePage" />
</template>

<style scoped></style>
