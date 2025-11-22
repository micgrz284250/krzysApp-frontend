<template>
  <div class="box">
    <p>Parametry Krzysia</p>
    <section class="parameter">
      <p>Energia: {{energia}}</p>
      <p>Tętno: {{tetno}}</p>
      <p>Temperatura: {{temperatura}}</p>
      <p>Nastrój: {{ formatNastroj(nastroj) }}</p>
    </section>
  </div>
</template>

<script setup>

defineProps({
  energia: Number,
  tetno: Number,
  temperatura: Number,
  nastroj: String,
});

function formatNastroj(nastroj) {
  switch (nastroj) {
    case 'SZCZESLIWY': return 'szczęśliwy';
    case 'ZANIEPOKOJONY': return 'zaniepojony';
    case 'SMUTNY': return 'smutny';
    case 'ZNUDZONY': return 'znudzony';
    case 'ZDENERWOWANY': return 'zdenerwowany';
    default: return 'nieznany';
  }
}

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