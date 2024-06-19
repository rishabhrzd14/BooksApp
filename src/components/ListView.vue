<template>
  <div>
    <h1>List of Books</h1>
    <input v-model="searchQuery" type="text" placeholder="Search for a book" />

    <div class="book-list">
      <div
        v-for="bookData in filteredBooksData"
        :key="bookData.id"
        class="book-item"
      >
        <ListItem :data="bookData" />
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { onMounted, ref, computed } from "vue";
import ListItem from "./ListItem.vue";

const booksData = ref([]);
const searchQuery = ref("");

const filteredBooksData = computed(() => {
  if (!searchQuery.value) {
    return booksData.value;
  }

  const query = searchQuery.value.toLowerCase();
  return booksData.value.filter((book) =>
    book.Title.toLowerCase().includes(query)
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
          "Access-Control-Allow-Origin": "*",
          "Content-Type": "application/json",
        }
      }
    );
    booksData.value = response.data.data;
  } catch (error) {
    console.error("Error fetching books data:", error);
  }
}
</script>

<style scoped>
.book-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.book-item {
  flex: 1 1 300px; /* Adjust as needed for your layout */
}

input[type="text"] {
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-bottom: 10px;
  width: 300px;
}

h1 {
  font-size: 24px;
  margin-bottom: 20px;
}
</style>
