<script setup>
    import { defineComponent, ref, getCurrentInstance, defineProps } from "vue";
import {
  Chart,
  Grid,
  Line,
  Bar,
  Marker,
  Tooltip,
  Pie,
  Responsive,
} from "vue3-charts";
import { dataBIG } from "./getAPI.vue";
let prop = defineProps(['year'])
let data = dataBIG.filter(s=> s.year== (prop.year||"2019")).map(s=> {s.race = String(s.materal_race_or_ethnicity || s.race); delete s.materal_race_or_ethnicity; return s})
</script>
<template>
<Chart
:size="{ width:420, height: 420 }"
:data="data"
:margin="{
      left: 0,
      top: 20,
      right: 20,
      bottom: 0
    }"
:direction="'circular'"
:axis="{
      primary: {
        type: 'band'
      },
      secondary: {
        domain: ['dataMin', 'dataMax + 1'],
        type: 'linear',
        ticks: 8
      }
    }"
:config="{ controlHover: false }"

>
<template #layers>
          <Pie
            :dataKeys="['race', 'infant_deaths']"
            :pie-style="{ innerRadius: 100, padAngle: 0.05 }" />
</template>
<template #widgets>
  <Tooltip
    borderColor="#48CAE4"
    :config="{
      race: { color: '#90e0ef' },
      infant_mortality_rate: { color: '#90e0ef' },
      postneonatal_mortality_rate: { color: '#0096c7' },
      neonatal_infant_deaths: { hide: true },
      neonatal_mortality_rate: { hide: true },
      postneonatal_infant_deaths: { hide: true },
    }"
  />
</template>
</Chart>
</template>

<style>
.widgets {
  position: absolute;
  top: 0px;
  left: 0px;
  min-height: 100px;
}
</style>