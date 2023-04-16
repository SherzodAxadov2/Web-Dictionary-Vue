<script setup>
import HomeHeader from "../components/home-header/HomeHeader.vue";
import FormSearch from "../components/form-search/FormSearch.vue";
import DictionaryWrapper from "../components/dictionary/DictionaryWrapper.vue";
import { ref } from "vue";

const definitionArray = ref([]);
async function getDefinition(word) {
  console.log(word);
  try {
    const url = "https://api.dictionaryapi.dev/api/v2/entries/en";

    const req = await fetch(`${url}/${word}`);
    const data = await req.json();
    definitionArray.value.splice(0, definitionArray.value.length);
    if (data[0]) {
      definitionArray.value.push(data[0]);
    }
  } catch (error) {
    console.log(error);
  }
  console.log(definitionArray.value[0]);
}
</script>

<template>
  <HomeHeader />
  <FormSearch @submit-word="getDefinition" />

  <div v-show="definitionArray.length > 0">
      <DictionaryWrapper :word="definitionArray[0]" />
  </div>

  <!-- <div class="loader">
    <div id="loading-bar-spinner" class="spinner">
      <div class="spinner-icon"></div>
    </div>
  </div>-->

  <!-- <div class="no_found container">
    <img src="assets/icons/sticker.png" alt="smile" />
    <p class="text-black-2d heading-s bold">No Definitions Found</p>
    <p class="body-m text-gray-bold">
      Sorry pal, we couldn't find definitions for the word you were looking for. You can
      try the search again at later time or head to the web instead.
    </p>
  </div> -->
</template>
