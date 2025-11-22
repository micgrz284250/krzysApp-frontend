<template>
  <div class="chart-container">
    <div>
      <Line
          id="energiaChart"
          :data="energiaData"
          :options="energiaChartOptions"
      />
    </div>
    <div>
      <Line
          ref="tetnoChart"
          :data="tetnoData"
          :options="tetnoChartOptions"
      />
    </div>
    <div>
      <Line
          ref="temperaturaChart"
          :data="temperaturaData"
          :options="temperaturaChartOptions"
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
  labels: [],
  datasets: [{
    label: 'Energia',
    backgroundColor: '#ff0000',
    borderColor: '#ff0000',
    data: []
  }]
});
const tetnoData = ref({
  labels: [],
  datasets: [{
    label: 'Tętno',
    backgroundColor: '#0000ff',
    borderColor: '#0000ff',
    data: []
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

const energiaChartOptions = {
  responsive: true,
  scales: {
    y: {
      min: 0,
      max: 100,
    }
  }
}
const tetnoChartOptions = {
  responsive: true,
  scales: {
    y: {
      min: 0,
      max: 200,
    }
  }
}
const temperaturaChartOptions = {
  responsive: true,
  scales: {
    y: {
      min: 0,
      max: 50,
    }
  }
}

function updateChart(krzys) {

  const newLabels = [... energiaData.value.labels];
  const newDataEnergia = [... energiaData.value.datasets[0].data];
  const newDataTetno = [... tetnoData.value.datasets[0].data];
  const newDataTemperatura = [... temperaturaData.value.datasets[0].data];

  if (newLabels.length >= 5) {
    newLabels.shift()
    newDataEnergia.shift()
    newDataTetno.shift()
    newDataTemperatura.shift()
  }

  const time = new Date(krzys.value.dateTime);

  newLabels.push(time.toLocaleTimeString('pl-PL', { hour: '2-digit', minute: '2-digit' , second: '2-digit' }));
  console.log(typeof krzys.value.dateTime);
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