<script setup lang="ts">
import { ref, onUnmounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const message: number = Number(route.params.msg) || 2

const currentTime = ref(Math.floor(Date.now() / 10))
const code = ref((message * 42) / currentTime.value)

const showCode = ref(false)

let intervalId: number

function showCodeFunction() {
  intervalId = setInterval(() => {
    currentTime.value = Math.floor(Date.now() / 1000)
    code.value = ((message * 42) / 2) * currentTime.value
  }, 1000)
  showCode.value = true
}

onUnmounted(() => {
  clearInterval(intervalId)
})
</script>

<template>
  <div class="new">
    <h1>Secret code:</h1>
    <br />
    <p v-if="showCode">
      {{ code }}
    </p>
    <button v-if="!showCode" @click="showCodeFunction">Get code</button>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .new {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
}
</style>
