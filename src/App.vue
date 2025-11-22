<script setup>
import { ref } from 'vue'
import TheHeader from './layouts/TheHeader.vue'
import TheMainCotent from './layouts/TheMainCotent.vue'
import TheSidebar from './layouts/TheSidebar.vue'
import candidates from '@/data/candidate-data.json'
//  Lưu vào storage
localStorage.setItem('candidateList', JSON.stringify(candidates))
</script>

<template>
  <div class="container display-flex flex-column">
    <TheHeader></TheHeader>
    <div class="content flex1 display-flex flex-row">
      <TheSidebar></TheSidebar>
      <TheMainCotent></TheMainCotent>
    </div>
  </div>
</template>
<style>
Reset css *,
body,
html {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Inter', Helvetica, Arial, sans-serif;
  font-size: 13px;
  overflow: hidden;
}

.container {
  width: 100%;
  /*  Lỗi fix sau */
  height: 100vh;
  /* background-color: aqua; */
  /* margin: 0 auto;
    padding: 20px; */
}
</style>
