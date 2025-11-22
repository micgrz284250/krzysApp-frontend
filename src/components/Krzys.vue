<template>
  <header>
    <h1 >Połączenie z Krzysiem</h1>
    <a :href="DATABASE_URL" target="_blank">Baza danych</a>
  </header>
  <body>
      <div class="box">
          <p>Wyślij komunikat do Krzysia</p>
          <input class="message" v-model="messageInput" type="text" @keyup.enter="postMessage($event.target.value)">
          <p v-show="flag" class="message">Wysłano wiadomość do Krzysia</p>
          <p v-show="flag" class="message">Treść wiadomości: {{ messageDisplay }}</p>
      </div>
      <div class="box">
        <BarChart ref="BarChartRef" />
        <p>Parametry Krzysia</p>
        <section class="parameter">
          <p>Energia: {{Krzys.energia}}</p>
          <p>Tętno: {{Krzys.tetno}}</p>
          <p>Temperatura: {{Krzys.temperatura}}</p>
          <p>Nastrój: {{Krzys.nastroj}}</p>
        </section>
      </div>
  </body>
</template>

<script setup>
import {onMounted, ref} from "vue";
import BarChart from "./Chart.vue";

const API_URL = 'http://localhost:8080';
const DATABASE_URL = API_URL+'/h2-console';

const Krzys = ref({
  id: 0,
  dateTime: 0,
  energia: 0,
  tetno: 0,
  temperatura: 0.0,
  nastroj: ""
});

const messageInput = ref("");
const messageDisplay = ref("");
let flag = false;

const BarChartRef = ref(null);

async function fetchVitals() {
  try {
    const response = await fetch(`${API_URL}/vitals`);
    Krzys.value = await response.json();
    console.log(Krzys.value);
    // przekażemy aktualne dane Krzysia do wykresu
    BarChartRef.value.updateChart(Krzys);
  } catch (error) {
    console.log(error);
  }
}

async function postMessage(content) {
  try {
    await fetch(`${API_URL}/message`, {
      method: 'POST',
      body: content
    })
    console.log(`Message send: ${messageInput.value}`)
    console.log(typeof content)
    messageDisplay.value = content;
    flag = true;
    setTimeout(() => {
      console.log("flag reset")
      flag = false;
    }, 3000);
  } catch (error) {
    console.log(error);
  }
  messageInput.value = "";
}

onMounted( () => {
  setInterval( () => {
    setTimeout(fetchVitals, 1000);
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
}

body {
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-items: center;
  align-items: center;
  height: 50vh;
}

.box {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}
</style>