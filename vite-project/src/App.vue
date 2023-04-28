


<template>
  <Chart
    :size="{ width: 900, height: 420 }"
    :data="data"
    :margin="margin"
    :direction="direction"
    :axis="axis">

    <template #layers>
      <Grid strokeDasharray="2,2" />
      <Bar :dataKeys="['race', 'infant_mortality_rate']" :barStyle="{ fill: '#90e0ef' }" />
      <Bar :dataKeys="['race', 'postneonatal_mortality_rate']" :barStyle="{ fill: '#0096c7' }" />
      <Marker :value="3" label="Avg." color="#e76f51" :strokeWidth="2" strokeDasharray="6 6" />
    </template>

    <template #widgets>
      <Tooltip
        borderColor="#48CAE4"
        :config="{
          race: { color: '#90e0ef' },
          infant_mortality_rate: { color: '#0096c7' },
          materal_race_or_ethnicity: {display: `none`}
        }"
      />
    </template>

  </Chart>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { Chart, Grid, Line, Bar, Marker,Tooltip } from 'vue3-charts'
import { data } from './getAPI.vue';
let data2019 = data.filter(s=> s.year == "2019").map(s=> {s.race = s.materal_race_or_ethnicity; return s})
    console.log(data2019)
export default defineComponent({
  name: 'BarChart',
  components: { Chart, Grid, Line,Bar,Marker,Tooltip },
  setup() {
    const data = data2019
    const direction = ref('horizontal')
    const margin = ref({
      left: 0,
      top: 20,
      right: 20,
      bottom: 0
    })

    const axis = ref({
      primary: {
        type: 'band'
      },
      secondary: {
        domain: ['dataMin', 'dataMax + 1'],
        type: 'linear',
        ticks: 8
      }
    })

    return { data, direction, margin, axis }
  }
})
</script>

<style>
.widgets {
  position: absolute;
  top: 0px;
  left: 0px;
}
</style>
