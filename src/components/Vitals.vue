<template>
  <div class="vitals-container">
    <h3>Parametry Krzysia</h3>
    <div class="parameter">
      <p>Energia: {{ energia }}</p>
      <p>Tętno: {{ tetno }}</p>
      <p>Temperatura: {{ temperatura }}</p>
      <p>Nastrój: {{ formatNastroj(nastroj) }}</p>
    </div>
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
.vitals-container {
  margin: 10px;
  background-color: gray;
  color: black;
  border-radius: 10px;
  padding: 10px;
}
</style>