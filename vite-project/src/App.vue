<script setup>
import point from './components/point.vue';
import barGraph from './components/barGraph.vue'
import pieChart from './components/pieChart.vue';
import { nextTick,ref } from 'vue';
let year = 2019
let renderComponent = ref(true)
const forceRerender = async () => {
  renderComponent.value = false;
	await nextTick();
  renderComponent.value = true;
}
let changeyear = function(x){
  year+=x
  console.log(year)
  forceRerender()
  
}
</script>
<template>
  <point @click="changeyear(-1)" :text="'Previous Year'" v-if="renderComponent"></point>
  <point @click="changeyear(1)" :text="'Next Year'" v-if="renderComponent"></point>
  <h2  v-if="renderComponent">{{ year }}</h2>
  <barGraph :year="year" v-if="renderComponent"></barGraph>
  <pieChart :year="year" v-if="renderComponent"></pieChart>

</template>




