<script setup>
const meanings = defineProps(["meaning"]);
console.log(meanings.meaning);
</script>

<template>
  <div class="dictionary__meanings">
    <div class="dictionary__part_of_speech">
      <p class="heading-m text-black-2d">{{ meanings.meaning.partOfSpeech }}</p>
      <span></span>
    </div>
    <div class="dictionary__meaning">
      <p class="heading-s text-gray-bold">Meaning</p>
      <ul>
        <li v-for="definition in meanings.meaning.definitions" :key="definition">
          <span></span>
          <div>
            <p class="body-m text-black-2d">
              {{ definition.definition }}
            </p>
            <p class="body-m text-gray-bold">
              {{ definition.example }}
            </p>
          </div>
        </li>
      </ul>
    </div>
    <div class="dictionary__synonym">
      <p class="heading-s text-gray-bold">Synonyms</p>
      <p class="heading-s text-purple bold">
        <a
          :href="
            meanings.meaning.synonyms[0]
              ? `https://en.wiktionary.org/wiki/` + meanings.meaning.synonyms[0]
              : 'https://en.wiktionary.org/wiki/'
          "
          target="_blank"
          >{{
            meanings.meaning.synonyms[0] ? meanings.meaning.synonyms[0] : "not found"
          }}</a
        >
      </p>
    </div>
  </div>
</template>
