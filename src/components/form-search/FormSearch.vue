<script setup>
import { ref } from "vue";

const word = ref("");
const error = defineProps(["error"]);

const placeholder = ref("Search for any word…");

const emit = defineEmits(["submit-word"]);
</script>

<template>
  <div class="container">
    <form
      :class="[error.error ? 'error' : '', 'form']"
      @submit.prevent="emit('submit-word', word.trim(''))"
    >
      <input type="text" class="form__input" v-model="word" :placeholder="placeholder" />
      <button type="submit" class="form__search">
        <img src="@/assets/icons/iconoir_search.png" alt="icon" />
      </button>
      <span class="heading-s text-red">Whoops, can’t be empty…</span>
    </form>
  </div>
</template>
