<script setup>
import HomeHeader from "../components/home-header/HomeHeader.vue";
import FormSearch from "../components/form-search/FormSearch.vue";
import DictionaryWrapper from "../components/dictionary/DictionaryWrapper.vue";
import { ref } from "vue";
import { useRouter, useRoute } from "vue-router";

const definitionArray = ref([]);
const loader = ref(false);
const nodata = ref(false);
const error = ref(false);
const showWord = ref(false);
const route = useRoute();
const router = useRouter();

const saveLocalStorage = (word) => {
  localStorage.setItem("word", word);
};

async function getDefinition(word) {
  loader.value = true;
  if (word) {
    query(word);
    showWord.value = false;
    error.value = false;
    nodata.value = false;
    try {
      const url = `${import.meta.env.VITE_APP_BASE_URL}/api/v2/entries/en`;
      const req = await fetch(`${url}/${word}`);
      const data = await req.json();
      definitionArray.value.splice(0, definitionArray.value.length);
      if (data.title) {
        query("");
        nodata.value = true;
        loader.value = false;
        return;
      }
      saveLocalStorage(data[0].word);
      nodata.value = false;
      definitionArray.value.push(data[0]);
      loader.value = false;
      showWord.value = true;
      loader.value = false;
    } catch (error) {
      console.error(error);
    }
  } else {
    query("");
    showWord.value = false;
    error.value = true;
    loader.value = false;
    nodata.value = false;
  }
}

const query = (word) => {
  router.replace({ query: { word: `${word}` } });
};

if (route.query.word) {
  getDefinition(route.query.word);
}
</script>

<template>
  <HomeHeader />
  <FormSearch @submit-word="getDefinition" :error="error" />
  <div v-if="showWord">
    <div v-if="definitionArray.length > 0">
      <DictionaryWrapper :word="definitionArray[0]" />
    </div>
  </div>

  <div class="loader" v-if="loader">
    <div id="loading-bar-spinner" class="spinner">
      <div class="spinner-icon"></div>
    </div>
  </div>

  <div v-if="nodata" class="no_found container nodata">
    <img src="@/assets/icons/sticker.png" alt="smile" />
    <p class="text-black-2d heading-s bold">No Definitions Found</p>
    <p class="body-m text-gray-bold">
      Sorry pal, we couldn't find definitions for the word you were looking for. You can
      try the search again at later time or head to the web instead.
    </p>
  </div>
</template>
