<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  modelValue: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["update:modelValue"]);

const name = ref(props.modelValue.name);
const description = ref(props.modelValue.description);
const image = ref(props.modelValue.image);
const genresInput = ref(props.modelValue.genres.join(", "));

watch(
  () => props.modelValue,
  (newVal) => {
    name.value = newVal.name;
    description.value = newVal.description;
    image.value = newVal.image;
    genresInput.value = newVal.genres.join(", ");
  }
);

function submitForm() {
  const genres = genresInput.value.split(",").map((g) => g.trim());
  emit("update:modelValue", {
    name: name.value,
    description: description.value,
    image: image.value,
    genres,
  });
}
</script>

<template>
  <div class="form-container">
    <h2 class="form-title">Add Movie</h2>
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
        <label for="genres" class="form-label">Genres (comma-separated):</label>
        <input
          type="text"
          id="genres"
          v-model="genresInput"
          required
          class="form-input"
        />
      </div>

      <button type="submit" class="submit-button">Add Movie</button>
    </form>
  </div>
</template>