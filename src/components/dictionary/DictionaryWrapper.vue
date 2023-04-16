<script setup>
import DictionaryHeader from "./DictionaryHeader.vue";
import DictionaryMeanings from "./DictionaryMeanings.vue";
import DictionarySource from "./DictionarySource.vue";

const data = defineProps(["word"]);
console.log(data.word);
</script>

<template>
  <div class="dictionary">
    <div class="container">
      <DictionaryHeader v-show="data.word" :word="data.word" />
      <DictionaryMeanings
        v-for="(meaning, index) in data.word.meanings"
        :key="index"
        :meaning="meaning"
      />

      <DictionarySource />
    </div>
  </div>
</template>
