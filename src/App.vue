<script setup>
import { ref, watch } from 'vue'
import axios from 'axios'

const API_URL = 'https://api-ssl.bitly.com/v4/shorten'
const link = ref()
const shortenedLink = ref()
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
}
</script>

<template>
  <div class="flex flex-col justify-center items-center gap-y-7	border border-black h-screen">
    <form @submit.prevent="onSubmit" class="flex flex-col gap-y-3 md:flex-row md:gap-x-3">
      <input class="bg-white border border-gray-400 rounded py-2 px-4" v-model="link" placeholder="Enter Link Here">
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Shorten Link</button>
    </form>
    <div v-if="isLinkGenerated" class="flex flex-col items-center gap-y-2">
      <div class="bg-white border border-gray-400 rounded py-2 px-4 mt-4">
        <p class="text-gray-800 font-semibold">Shortened Link:</p>
        <a :href="shortenedLink" class="text-blue-500 hover:text-blue-700 font-medium">{{ shortenedLink }}</a>
      </div>
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="onCopy">Copy Shortened
        Link</button>
    </div>
  </div>
</template>

