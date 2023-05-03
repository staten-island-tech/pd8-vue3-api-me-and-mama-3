<script setup >
let prop = defineProps(['text'])

</script>
<template>
  <button>
      {{prop.text}}
    </button>
</template>