<script setup>
let prop = defineProps(["text"]);
</script>
<template>
  <button>
    {{ prop.text }}
  </button>
</template>

<style>
button {
  background-color: rgb(170, 170, 170);
  border-radius: 1rem;
  z-index: 2;
}
</style>
