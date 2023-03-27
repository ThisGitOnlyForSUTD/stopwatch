<template>
  <div class="main">
    <section class="container">
    <app-card v-for="(timer, idx) in timerCount" :key="timer+idx"/>
    <button @click="timerCount++" class="add">
      <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect x="8.5" width="3" height="20" fill="#FFFFFF"/>
        <rect y="11.5" width="3" height="20" transform="rotate(-90 0 11.5)" fill="#FFFFFF"/>
      </svg>
    </button>
  </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import AppCard from './components/AppCard.vue'
const timerCount = ref(1)
</script>

<style scoped>
.main {
  width: 100%;
  margin: 0 auto;
  display: flex;
  justify-content: center;
}
.container {
  display: flex;
  width: 100%;
  justify-content: flex-start;
  flex-wrap: wrap;
  gap: 45px 50px;
}


@media (max-width: 560px) {
   .container {
    justify-content: center;
    gap: 45px 0;
    flex-direction: column;
   } 
  }
  @media (max-width: 831px) {
   .container {
    max-width: 500px;
    align-content: center;
    justify-content: flex-start;
    gap: 45px;
   } 
  }
.add {
  padding: 20px 0;
  width: 225px;
  height: 120px;
  background: #696969;
  color: #FFFFFF;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  opacity: 0.7;
}

.add:hover {
  opacity: 1;
}
</style>