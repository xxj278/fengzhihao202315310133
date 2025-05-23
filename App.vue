<template>
  <div id="app">
    <div class="chart-row">
      <BarChart ref="barChart" class="chart-item" />
      <LineChart ref="lineChart" class="chart-item" />
    </div>
    <div class="chart-row">
      <PieChart ref="pieChart" class="chart-item" />
      <!-- <MapChart ref="mapChart" class="chart-item" /> -->
    </div>
  </div>
</template>

<script>
import BarChart from "./components/BarChart.vue";
import LineChart from "./components/LineChart.vue";
import PieChart from "./components/PieChart.vue";
// import MapChart from "./components/MapChart.vue";
import axios from "axios";

export default {
  components: {
    BarChart,
    LineChart,
    PieChart,
    // MapChart,
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get("/data.json");
        const data = response.data;

        this.$refs.barChart.updateData(data.regionPower);
        this.$refs.lineChart.updateData(data.powerTrend);
        this.$refs.pieChart.updateData(data.energyMix.data);
        // this.$refs.mapChart.updateData(data.stationMap.data);
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
  },
};
</script>

<style>
#app {
  width: 100%;
  display: flex;
  flex-direction: column;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.chart-row {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.chart-item {
  width: calc(50% - 10px); /* Adjust for spacing */
  height: 400px;
  box-sizing: border-box;
}
</style>