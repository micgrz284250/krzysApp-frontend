<script setup>

import {inject, ref} from "vue";

const API_URL = inject('API_URL');

const messageInput = ref("");
const messageDisplay = ref("");
let flag = false;

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

</script>

<template>
  <p>Wyślij komunikat do Krzysia</p>
  <input class="message" v-model="messageInput" type="text" @keyup.enter="postMessage($event.target.value)">
  <p v-show="flag" class="message">Wysłano wiadomość do Krzysia</p>
  <p v-show="flag" class="message">Treść wiadomości: {{ messageDisplay }}</p>
</template>

<style scoped>

</style>