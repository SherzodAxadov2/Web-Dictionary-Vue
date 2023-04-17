<script setup>
import { ref } from "vue";

const data = defineProps(["word"]);

function audioPlay() {
  let audio = ref("");
  data.word.phonetics.map((phonetic) => {
    if (phonetic.audio) {
      audio.value = new Audio(phonetic.audio);
    }
  });

  audio.value.play();
}
</script>

<template>
  <div class="dictionary__header">
    <div class="dictionary__word">
      <h1 class="heading-l text-black-2d">
        {{ data.word.word }}
      </h1>
      <p class="dictionary__spelling heading-m text-purple"></p>
    </div>

    <button class="dictionary__audio" @click="audioPlay">
      <i class="fa-sharp fa-solid fa-play"></i>
    </button>
  </div>
</template>
