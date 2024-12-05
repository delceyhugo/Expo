<script setup>
import { onMounted, ref } from 'vue';
// Pages
import Hero from './pages/Hero.vue'
import Archive from './pages/Archive.vue'
// Components
import Cursor from './components/Cursor.vue'

const activePage = ref(["hero"])



const changePage = (page) => {
  activePage.value = [activePage.value[0], page]

  const activePageEl = document.querySelector(`#${activePage.value[0]}`)
  activePageEl.scrollIntoView({ behavior: "smooth", block: "center"})

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
    activePage.value = [page]
  }, 2000)
}

</script>

<template>
  <Cursor />
  <Hero class="page" @changePage="changePage"/>
  <Archive class="page" @changePage="changePage"/>
</template>

<style lang="scss" scoped>

</style>
