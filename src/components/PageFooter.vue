Copyright (c) {{ currentYear }} ATBSPB. Licensed under the MIT License.

<template>
  <footer :style="{ opacity: footerOpacity }">
    Copyright &copy; {{ currentYear }} ATBSPB. All rights reserved.
    <br />
    Powered by <a href="https://www.netlify.com" target="_blank">Netlify</a> &amp; <a href="https://zyyo.net/" target="_blank">zyyo</a>
  </footer>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const currentYear = ref(new Date().getFullYear())
const footerOpacity = ref(0)

const FADE_THRESHOLD = 300

function handleScroll() {
  const scrollTop = window.scrollY || document.documentElement.scrollTop
  const windowHeight = window.innerHeight
  const documentHeight = document.documentElement.scrollHeight
  const distanceFromBottom = documentHeight - (scrollTop + windowHeight)

  if (distanceFromBottom <= 0) {
    footerOpacity.value = 1
  } else if (distanceFromBottom >= FADE_THRESHOLD) {
    footerOpacity.value = 0
  } else {
    footerOpacity.value = 1 - distanceFromBottom / FADE_THRESHOLD
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>