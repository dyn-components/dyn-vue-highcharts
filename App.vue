<script setup lang="ts">
import DynComponent from "./src";
import Highcharts from "highcharts";

const options: Highcharts.Options = {
  accessibility: {
    enabled: false,
  },
  credits: { enabled: false },
  chart: {
    type: "pie",
    backgroundColor: "rgba(0,0,0,0)",
    options3d: {
      enabled: true,
      alpha: 50,
    },
  },
  legend: {
    align: "left",
    verticalAlign: "top",
    itemStyle: {
      color: "#fff",
      fontSize: "14px",
      lineHeight: "30px",
    },
    enabled: false,
  },
  title: {},
  plotOptions: {
    pie: {
      innerSize: 50,
      depth: 40,
      allowPointSelect: true,
      cursor: "pointer",
      dataLabels: {
        enabled: true,
        format: "<b>{point.name}</b>({point.y})<br \> {point.percentage:.1f}%",
      },
      showInLegend: true,
    },
  },
  series: [
    {
      type: "pie",
      name: "数量",
      data: [
        ["活跃", 100],
        ["不活跃", 200],
      ],
    },
  ],
};
</script>

<template>
  <main class="dyn-container">
    <DynComponent class="dyn-component" :options="options" />
  </main>
</template>

<style lang="scss" scoped>
.dyn-container {
  width: 100%;
  height: 500px;
}
</style>
