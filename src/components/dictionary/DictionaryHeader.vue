<script setup>
const data = defineProps(["word"]);
</script>

<template>
  <div class="dictionary__header">
    <div class="dictionary__word">
      <h1 class="heading-l text-black-2d">
        {{ data.word.word }}
      </h1>
      <p class="dictionary__spelling heading-m text-purple">
        {{ data.word.phonetics[1].text }}
      </p>
    </div>
    <button class="dictionary__audio">
      <i class="fa-sharp fa-solid fa-play"></i>
    </button>
  </div>
</template>
