<template>
  <Line
      ref="vitalsChartRef"
      :data="chartData"
      :options="chartOptions"
  />
</template>

<script setup>
import {Line} from 'vue-chartjs'
import {Chart as ChartJS, Legend, LinearScale, LineElement, PointElement, Title, Tooltip, CategoryScale} from 'chart.js'
import {ref} from "vue";

ChartJS.register(CategoryScale, LinearScale, PointElement, LineElement, Title, Tooltip, Legend)

defineExpose({ updateChart })

const vitalsChartRef = ref(null)

const chartData = ref({
  labels: [0, 0, 0, 0, 0],
  datasets: [
    {
      label: 'Energia',
      backgroundColor: '#ff0000',
      borderColor: '#ff0000',
      data: [0, 0, 0, 0, 0]
    },
    {
      label: 'Tętno',
      backgroundColor: '#0000ff',
      borderColor: '#0000ff',
      data: [0, 0, 0, 0, 0]
    },
    {
      label: 'Temperatura',
      backgroundColor: '#00ff00',
      borderColor: '#00ff00',
      data: [0, 0, 0, 0, 0]
    }
  ]
});

const chartOptions = {
  responsive: true
}

function updateChart(krzys) {

  const newLabels = [... chartData.value.labels];
  const newDataEnergia = [... chartData.value.datasets[0].data];
  const newDataTetno = [... chartData.value.datasets[1].data];
  const newDataTemperatura = [... chartData.value.datasets[2].data];

  if (chartData.value.labels.length >= 5){
    newLabels.shift()
    newDataEnergia.shift()
    newDataTetno.shift()
    newDataTemperatura.shift()
  }
  newLabels.push(krzys.value.id);
  chartData.value.labels = newLabels;
  // Energia
  newDataEnergia.push(krzys.value.energia);
  chartData.value.datasets[0].data = newDataEnergia;
  // Tętno
  newDataTetno.push(krzys.value.tetno);
  chartData.value.datasets[1].data = newDataTetno;
  // Temperatura
  newDataTemperatura.push(krzys.value.temperatura);
  chartData.value.datasets[2].data = newDataTemperatura;

  console.log(chartData.value);

  chartData.value = {
    labels: newLabels,
    datasets: [
      {
        label: 'Energia',
        backgroundColor: '#ff0000',
        borderColor: '#ff0000',
        data: newDataEnergia
      },
      {
        label: 'Tętno',
        backgroundColor: '#0000ff',
        borderColor: '#0000ff',
        data: newDataTetno
      },
      {
        label: 'Temperatura',
        backgroundColor: '#00ff00',
        borderColor: '#00ff00',
        data: newDataTemperatura
      }
    ]
  }
}

</script>