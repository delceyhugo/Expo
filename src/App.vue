<script setup>
import { onMounted, ref } from 'vue';
// Pages
import Hero from './pages/Hero.vue'
import Archive from './pages/Archive.vue'
// Components
import Cursor from './components/Cursor.vue'



const changePage = (page) => {
  // Animation
  document.querySelectorAll(`.page`).forEach((el) => {
    el.classList.add('change-page')
  })

  // Scroll
  setTimeout(() => {
    let nextPageEl = document.querySelector(`#${page}`)
    nextPageEl.scrollIntoView({ behavior: "smooth", block: "center"})
  }, 1000)

  // Remove animation
  setTimeout(() => {
    document.querySelectorAll(`.page`).forEach((el) => {
    el.classList.remove('change-page')
  })
  }, 2000)
}

</script>

<template>
  <Cursor />
  <Hero class="page" @changePage="changePage"/>
  <Archive class="page"/>
</template>

<style lang="scss" scoped>

</style>
