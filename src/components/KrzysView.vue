<script setup>
import { ref } from "vue";
const API_URL = 'http://localhost:8080';

const vitals = ref(null);

async function fetchVitals() {
  try {
    const response = await fetch(`${API_URL}/vitals`);
    vitals.value = await response.json();
    console.log(vitals.value);
  } catch (error) {
    console.log(error);
  }
}
</script>

<template>
  <div class="container-header">
    <header>
      <h1 >Połączenie z Krzysiem</h1>
    </header>
  </div>
  <div class="container-body">
    <div class="box">
      <main>
        <p>Wyślij komunikat do Krzysia</p>
        <input class="message" type="text">
      </main>
    </div>
    <div class="box">
      <p>Parametry Krzysia</p>
      <section class="parameter">
        <p>Energia: {{energia}}</p>
        <p>Tętno: {{tetno}}</p>
        <p>Temperatura: {{temperatura}}</p>
        <p>Nastrój: {{nastroj}}</p>
      </section>
      <button class="parameter" @click="fetchVitals">Odśwież parametry życiowe Krzysia</button>
    </div>
  </div>
</template>

<style scoped>
.container-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-decoration: none;
  color: black;
  background-color: gray;
  border-radius: 10px;
}

.container-body {
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

.parameter {
  text-align: left;
}

input.message {
  text-align: center;
  padding: 10px;
}

button.parameter {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 6px 14px;
  border-radius: 6px;
  border: none;
}
</style>