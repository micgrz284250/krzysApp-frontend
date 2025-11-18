<template>
  <Bar id="vitals-bar" :option="chartOptions" :data="chartData" />
</template>

<script setup>
import { Bar } from "vue-chartjs"
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'



</script>

<style scoped>

</style>