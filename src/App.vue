<script setup>
import { ref, watch } from 'vue'
import axios from 'axios'

const API_URL = 'https://api-ssl.bitly.com/v4/shorten'
const link = ref()
const shortenedLink = ref()

const onSubmit = async () => {
  const response = await axios.post(API_URL, {
    long_url: link.value,
    domain: 'bit.ly',
  }, {
    headers: {
      'Content-Type': 'application/json',
      'Authorization': 'Bearer 90ed93ecb8217e196a639ab725cf0af8659eb580'
    }
  })
  shortenedLink.value = response.data.link
}
</script>

<template>
  <form @submit.prevent="onSubmit">
    <input v-model="link" placeholder="Enter Link Here">
    <button>Shorten Link</button>
  </form>
  <p>{{ shortenedLink }}</p>
</template>

