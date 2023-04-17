<script setup>
const url = defineProps(["source"]);
</script>

<template>
  <div class="dictionary__source">
    <a :href="url.source" target="_blank" class="body-s text-gray-bold">Source</a>
    <a :href="url.source" target="_blank" class="body-s text-black-2d">{{
      url.source[0]
    }}</a>
    <a :href="url.source" target="_blank"
      ><i class="fa-solid fa-arrow-up-right-from-square"></i
    ></a>
  </div>
</template>
