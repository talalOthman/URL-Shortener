<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import { ref, watchEffect } from 'vue'

const link = ref()
const onSubmit = () => console.log("Working...")
</script>

<template>
  <form @submit.prevent="onSubmit">
    <input v-model="link" placeholder="Enter Link Here">
    <button>Shorten Link</button>
  </form>
</template>

