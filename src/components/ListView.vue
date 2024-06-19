<template>
  <h1>List of Books</h1>
  <input v-model="searchQuery" type="text" placeholder="Search for a book" />

  <div v-for="bookData in filteredBooksData">
    <ListItem :key="bookData.id" :data="bookData" />
  </div>
</template>
<script setup>
import axios from "axios";
import { onMounted, ref, computed } from "vue";
import ListItem from "./ListItem.vue";

const booksData = ref([]);
const searchQuery = ref("");
const filteredBooksData = computed(() => {
  if (!searchQuery.value && !booksData.value.length) {
    return booksData.value;
  }

  return booksData.value.filter((book) =>
    book.Title.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});
onMounted(() => {
  fetchData();
});

async function fetchData() {
  try {
    const response = await axios.get(
      "https://stephen-king-api.onrender.com/api/books",
      {
        headers: {
          "Content-Type": "application/json",
          "Access-Control-Allow-Origin": "*",
          "Access-Control-Allow-Methods":
            "GET, POST, PATCH, PUT, DELETE, OPTIONS",
          "Access-Control-Allow-Headers":
            "Origin, Content-Type, X-Auth-Token, Authorization, Accept,charset,boundary,Content-Length",
          "Access-Control-Expose-Headers": "Authorization,Access-Token, Uid",
        },
      }
    );
    booksData.value = response.data.data;
  } catch (error) {
    console.error("Error fetching books data:", error);
  }
}
</script>
<style></style>
