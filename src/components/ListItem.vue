<template>
  <div class="book-card">
    <h2 class="title">{{ data.Title }}</h2>
    <p><strong>Year:</strong> {{ data.Year }}</p>
    <p><strong>Publisher:</strong> {{ data.Publisher }}</p>
    <p><strong>ISBN:</strong> {{ data.ISBN }}</p>
    <p><strong>Pages:</strong> {{ data.Pages }}</p>
    <p><strong>Notes:</strong> {{ data.Notes && data.Notes.length > 0 ? data.Notes.join(', ') : 'Not available' }}</p>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  data: {
    type: Object,
    default: () => ({}),
  },
});

// Log the props data to the console
console.log(props.data, "book-data");
</script>

<style scoped>
.book-card {
  display: flex;
  flex-direction: column;
  border: 1px solid #e0e0e0;
  padding: 10px;
  margin: 10px;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  color: #333;
  text-align: left;
  width: 320px;
  height: 300px;
  font-family: 'Arial', sans-serif;
}

.title {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 10px;
  font-size: 1.5em;
}

p {
  margin: 2.5px 0;
}

p strong {
  color: #2980b9;
}
</style>