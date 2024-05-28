<script setup lang="ts">
const pages: number[] = [1, 2];

export interface currentPageProps {
  currentPage: number;
}
defineProps<currentPageProps>();

const emit = defineEmits<{
  (e: "changePage", page: number): void;
}>();
</script>

<template>
  <section>
    <button
      v-for="(page, i) in pages"
      :key="i"
      @click="$emit('changePage', page)"
      :class="{ activePage: page === currentPage }"
    >
      {{ page }}
    </button>
  </section>
</template>

<style scoped>
section {
  display: flex;
  gap: 1em;
}

button {
  height: 3em;
  width: 3em;
  border-radius: 50%;
  border: none;
  background-color: rgb(81, 94, 81);
  color: white;
  font-weight: bold;
  font-size: 1em;
}

button:hover {
  border: 3px solid rgb(205, 228, 205);
}

.activePage {
  background-color: rgb(127, 150, 127);
  border: 3px solid rgb(205, 228, 205);
}
</style>
