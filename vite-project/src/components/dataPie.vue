<template>
  <Chart
    direction="circular"
    :size="{ width: 400, height: 400 }"
    :data="data"
    :margin="{
      left: Math.round((400 - 360) / 2),
      top: 20,
      right: 0,
      bottom: 20,
    }"
    :axis="axis"
    :config="{ controlHover: false }"
  >
    <template #layers>
      <Pie
        :dataKeys="['race', 'infant_deaths']"
        :barStyle="{ fill: '#0096c7' }"
        :pie-style="{ innerRadius: 100, padAngle: 0.05 }"
      />
    </template>
    <template #widgets>
      <Tooltip
        :config="{
          name: {},
          infant_deaths: {},
          neonatal_infant_deaths: { hide: true },
          neonatal_mortality_rate: { hide: true },
          postneonatal_infant_deaths: { hide: true },
          postneonatal_mortality_rate: { hide: true },
          year: { hide: true },
        }"
        hideLine
      />
    </template>
  </Chart>
</template>

<script>
import { defineComponent, ref } from "vue";
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
let data2019 = dataBIG
  .filter((s) => s.year == "2019")
  .map((s) => {
    s.race = String(s.materal_race_or_ethnicity);
    delete s.materal_race_or_ethnicity;
    return s;
  });
console.log(data2019);
export default defineComponent({
  name: "Boobies",
  components: { Pie, Chart, Grid, Line, Bar, Marker, Tooltip },
  methods: {
    changeYear: async function (year) {
      data = dataBIG((s) => s.year == year).map((s) => {
        s.race = String(s.materal_race_or_ethnicity);
        delete s.materal_race_or_ethnicity;
        return s;
      });
    },
  },
  setup() {
    let data = data2019;
    const direction = ref("horizontal");
    const margin = ref({
      left: 0,
      top: 20,
      right: 20,
      bottom: 0,
    });
    const axis = ref({
      primary: {
        type: "band",
      },
      secondary: {
        domain: ["dataMin", "dataMax + 1"],
        type: "linear",
        ticks: 8,
      },
    });

    return { data, direction, margin, axis };
  },
});
</script>
