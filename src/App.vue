<script setup>
import { ref, watch } from 'vue'
import axios from 'axios'

const API_URL = 'https://api-ssl.bitly.com/v4/shorten'
const link = ref()
const shortenedLink = ref()
const copyButton = ref('Copy Shortened Link')
const isLinkGenerated = ref(false)

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
  isLinkGenerated.value = true
}

const onCopy = () => {
  navigator.clipboard.writeText(shortenedLink.value)
  copyButton.value = 'Copied!'
  setTimeout(() => {
    copyButton.value = 'Copy Shortened Link'
  }, 2000)
}
</script>

<template>
  <div
    class="flex flex-col justify-center items-center gap-y-7	border border-gray-300 h-screen bg-gradient-to-br from-blue-200 to-blue-300">
    <div class="flex flex-col items-center">
      <h1 class="text-3xl font-bold text-gray-800 mb-4">URL Shortener</h1>
      <p class="text-gray-700 text-lg text-center">Enter a long URL below to generate a shortened link</p>
    </div>
    <form @submit.prevent="onSubmit"
      class="flex flex-col gap-y-3 md:flex-row md:gap-x-3 px-4 py-6 bg-white rounded-lg shadow-md">
      <input class="bg-gray-100 border border-gray-400 rounded py-2 px-4" v-model="link" placeholder="Enter Link Here">
      <button
        class="bg-blue-700 hover:bg-blue-800 text-white font-bold py-2 px-4 rounded transition duration-200 ease-in-out transform hover:scale-105">Shorten
        Link</button>
    </form>
    <div v-if="isLinkGenerated" class="flex flex-col items-center gap-y-2 mt-6">
      <div class="bg-gray-100 border border-gray-400 rounded py-2 px-4">
        <p class="text-gray-800 font-semibold">Shortened Link:</p>
        <a :href="shortenedLink" class="text-blue-500 hover:text-blue-700 font-medium">{{ shortenedLink }}</a>
      </div>
      <button
        class="bg-blue-700 hover:bg-blue-800 text-white font-bold py-2 px-4 rounded transition duration-200 ease-in-out transform hover:scale-105 mt-4"
        @click="onCopy">{{copyButton}}</button>
    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

body {
  font-family: 'Montserrat', sans-serif;
}
</style>








