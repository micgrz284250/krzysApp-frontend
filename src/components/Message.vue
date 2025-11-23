<template>
  <div class="message-container">
    <h3>Wyślij komunikat do Krzysia</h3>
    <input class="message" v-model="messageInput" type="text" @keyup.enter="postMessage($event.target.value)">
    <p v-show="flag" class="message-info">Wysłano wiadomość do Krzysia</p>
    <p v-show="flag" class="message-info">Treść wiadomości: {{ messageDisplay }}</p>
  </div>
</template>

<script setup>

import {inject, ref} from "vue";

const API_URL = inject('API_URL');

const messageInput = ref("");
const messageDisplay = ref("");
const flag = ref(false);

async function postMessage(content) {
  try {
    await fetch(`${API_URL}/message`, {
      method: 'POST',
      body: content
    })
    console.log(`Message send: ${messageInput.value}`)
    console.log(typeof content)
    messageDisplay.value = content;
    flag.value = true;
    setTimeout(() => {
      console.log("flag reset")
      flag.value = false;
    }, 3000);
  } catch (error) {
    console.log(error);
  }
  messageInput.value = "";
}

</script>

<style scoped>
.message-container {
  display: flex;
  flex-direction: column;
}
</style>