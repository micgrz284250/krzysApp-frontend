<template>
  <header>
    <h1 >Połączenie z Krzysiem</h1>
    <a :href="DATABASE_URL" target="_blank">Baza danych</a>
  </header>
  <body>
  <Chart ref="chart" />
  <Vitals :energia="Krzys.energia" :tetno="Krzys.tetno" :temperatura="Krzys.temperatura" :nastroj="Krzys.nastroj" />
  <Message/>
  </body>
</template>

<script setup>
  import Vitals from "@/components/Vitals.vue";
  import Message from "@/components/Message.vue";
  import Chart from "@/components/Chart.vue";
  import {onMounted, provide, ref} from "vue";

  const API_URL = 'http://localhost:8080';
  const DATABASE_URL = API_URL+'/h2-console';

  provide('API_URL', API_URL);
  provide('DATABASE_URL', DATABASE_URL);

  const chart = ref(null);

  const Krzys = ref({
    id: 0,
    time: 0,
    energia: 0,
    tetno: 0,
    temperatura: 0,
  });

  async function fetchVitals() {
    try {
      const response = await fetch(`${API_URL}/vitals`);
      Krzys.value = await response.json();
      console.log(Krzys.value);
    } catch (error) {
      console.log(error);
    }
  }

  onMounted( () => {
    fetchVitals();
    setInterval( () => {
      fetchVitals();
      chart.value.updateChart(Krzys);
    }, 5000);
  });

</script>

<style scoped>
header {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-decoration: none;
  color: black;
  background-color: gray;
  border-radius: 10px;
  padding: 5px;
}

header h1 {
  font-size: 30px;
}

header a {
  font-size: 20px;
  color: darkblue;
}

@media (hover: hover) and (pointer: fine) {
  header a:hover {
    color: aqua;
  }
}

body {
  display: flex;
  flex-direction: column;
  align-items: center;
}

</style>