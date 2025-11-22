<template>
  <div class="chart-container">
    <div>
      <Line
          id="energiaChart"
          :data="energiaData"
          :options="chartOptions"
      />
    </div>
    <div>
      <Line
          ref="tetnoChart"
          :data="tetnoData"
          :options="chartOptions"
      />
    </div>
    <div>
      <Line
          ref="temperaturaChart"
          :data="temperaturaData"
          :options="chartOptions"
      />
    </div>
  </div>
</template>

<script setup>
import {Line} from 'vue-chartjs'
import {Chart as ChartJS, Legend, LinearScale, LineElement, PointElement, Title, Tooltip, CategoryScale} from 'chart.js'
import {ref} from "vue";

ChartJS.register(CategoryScale, LinearScale, PointElement, LineElement, Title, Tooltip, Legend)

defineExpose({ updateChart })

const energiaData = ref({
  labels: [0, 0, 0, 0, 0],
  datasets: [{
    label: 'Energia',
    backgroundColor: '#ff0000',
    borderColor: '#ff0000',
    data: [0, 0, 0, 0, 0]
  }]
});
const tetnoData = ref({
  labels: [0, 0, 0, 0, 0],
  datasets: [{
    label: 'Tętno',
    backgroundColor: '#0000ff',
    borderColor: '#0000ff',
    data: [0, 0, 0, 0, 0]
  }]
});
const temperaturaData = ref({
  labels: [],
  datasets: [{
    label: 'Temperatura',
    backgroundColor: '#00ff00',
    borderColor: '#00ff00',
    data: []
  }]
});

const chartOptions = {
  responsive: true
}

function updateChart(krzys) {

  const newLabels = [... energiaData.value.labels];
  const newDataEnergia = [... energiaData.value.datasets[0].data];
  const newDataTetno = [... tetnoData.value.datasets[0].data];
  const newDataTemperatura = [... temperaturaData.value.datasets[0].data];

  newLabels.shift()
  newDataEnergia.shift()
  newDataTetno.shift()
  newDataTemperatura.shift()

  newLabels.push(krzys.value.id);

  // Energia
  newDataEnergia.push(krzys.value.energia);
  // Tętno
  newDataTetno.push(krzys.value.tetno);
  // Temperatura
  newDataTemperatura.push(krzys.value.temperatura);

  energiaData.value = {
    labels: newLabels,
    datasets: [{
      label: 'Energia',
      backgroundColor: '#ff0000',
      borderColor: '#ff0000',
      data: newDataEnergia
    }]
  };
  tetnoData.value = {
    labels: newLabels,
    datasets: [{
      label: 'Tętno',
      backgroundColor: '#0000ff',
      borderColor: '#0000ff',
      data: newDataTetno
    }]
  };
  temperaturaData.value = {
    labels: newLabels,
    datasets: [{
      label: 'Temperatura',
      backgroundColor: '#00ff00',
      borderColor: '#00ff00',
      data: newDataTemperatura
    }]
  };
}

</script>

<style scoped>
.chart-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  justify-items: center;
  align-items: center;
}
</style>