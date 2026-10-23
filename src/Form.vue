<script setup>
import { ref } from "vue";

const emit = defineEmits(["add-movie", "close"]);

const name = ref("");
const description = ref("");
const image = ref("");
const genresInput = ref("");

function submitForm() {
  const genres = genresInput.value.split(",").map((g) => g.trim());
  emit("add-movie", {
    name: name.value,
    description: description.value,
    image: image.value,
    genres,
  });
}
function closeAddMovieDialog() {
  emit("close");
}
</script>

<template>
  <div class="form-container">
<div class="form-header">
      <h2 class="form-title">Add Movie</h2>
      <button type="button" class="icon-close-button" @click="closeAddMovieDialog">✕</button>
    </div>
    <form @submit.prevent="submitForm" class="form">
      <div class="form-field">
        <label for="name" class="form-label">Name:</label>
        <input
          type="text"
          id="name"
          v-model="name"
          required
          class="form-input"
        />
      </div>

      <div class="form-field">
        <label for="description" class="form-label">Description:</label>
        <textarea
          id="description"
          v-model="description"
          required
          class="form-textarea"
        ></textarea>
      </div>

      <div class="form-field">
        <label for="image" class="form-label">Image URL:</label>
        <input
          type="text"
          id="image"
          v-model="image"
          required
          class="form-input"
        />
      </div>

      <div class="form-field">
        <label for="genres" class="form-label">Genres <span class="form-hint">(comma-separated)</span></label>
        <input
          type="text"
          id="genres"
          v-model="genresInput"
          required
          class="form-input"
        />
      </div>
      <div class="form-actions">
        <button type="button" class="button button-secondary" @click="closeAddMovieDialog">
          Cancel
        </button>
        <button type="submit" class="button button-primary">
          Add Movie
        </button>
      </div>
    </form>
  </div>
</template>