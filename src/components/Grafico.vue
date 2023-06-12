<script setup>
import Chart from "chart.js/auto";
import { ref, onMounted } from "vue";

const props = defineProps(["xAxis", "yAxis", "label"]);

const canvas = ref(null);

const chartConfig = {
  type: "line",
  data: {
    labels: props.xAxis,
    datasets: [
      {
        label: props.label,
        data: props.yAxis,
        pointStyle: 'circle',
        pointRadius: 8,
        pointHoverRadius: 12
      },
    ],
  },
};

onMounted(() => {
  canvas.value = document.querySelector("canvas");
  new Chart(canvas.value, chartConfig);
});
</script>

<template>
  <div class="w-[800px] bg-white rounded-md">
    <canvas ref="canvas"></canvas>
  </div>
</template>
