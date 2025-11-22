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
</style>