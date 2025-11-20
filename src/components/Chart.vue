<template>
  <Line
      id="vitals-chart"
      :options="chartOptions"
      :data="chartData"
  />
</template>

<script setup>
import { ref } from 'vue'
import { Line } from 'vue-chartjs'
import { Chart as ChartJS, CategoryScale, LinearScale, PointElement, LineElement, Title, Tooltip, Legend } from 'chart.js'

ChartJS.register(CategoryScale, LinearScale, PointElement, LineElement, Title, Tooltip, Legend)

const chartData = ref({
  labels: [],
  datasets: [
    {
      label: 'Energia',
      backgroundColor: '#ff0000',
      data: []
    },
    {
      label: 'Tętno',
      backgroundColor: '#0000ff',
      data: []
    },
    {
      label: 'Temperatura',
      backgroundColor: '#00ff00',
      data: []
    }
  ]
})

const chartOptions = {
  responsive: true
}
</script>