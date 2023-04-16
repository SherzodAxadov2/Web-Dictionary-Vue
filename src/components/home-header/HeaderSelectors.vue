<script setup>
const props = defineProps(["selector"]);
</script>

<template>
  <li>
    <p class="body-m text-black-2d" onclick="setSelectorValue(event)">
      {{ props.selector }}
    </p>
  </li>
</template>
