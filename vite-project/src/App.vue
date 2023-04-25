
<script setup>
    import { data } from './getAPI.vue'
    import App from "./App.vue"
    import { createApp } from 'vue'
    console.log(data)
    const app = createApp()
    app.component("Point",Point)

</script>
<script>
    import Point from './components/point.vue';

export default {
  components: {
    Point
  }
}
</script>


<template>
    <Point />
</template>
<script>
</script>
<style scoped>
</style>
