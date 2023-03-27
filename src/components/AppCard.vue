<template>
  <div class="card" :style="[active ? {'opacity': '1'} : {'opacity': '0.8'}]">
    <span class="card__time" >
      <span class="stop-watch__timer-hours"  v-if="hh > 0"> {{ hh }} : </span>
        <span class="stop-watch__timer-minutes" v-if="min > 0" > {{ min }} : </span>
        <span class="stop-watch__timer-seconds"> {{ seg }} </span>
    </span>
    <div class="card__btns">
      <app-btn>
        <svg @click="startTimer" v-if="active == false" width="17" height="20" viewBox="0 0 17 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 20V0L17 10L0 20Z" fill="#FFF"/>
        </svg>
        <svg @click="stopTimer" v-if="active == true" width="10" height="20" viewBox="0 0 10 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="7" width="3" height="20" fill="#FFF"/>
          <rect width="3" height="20" fill="#FFF"/>
        </svg>
      </app-btn>
      <app-btn @click="restartTimer">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect width="20" height="20" fill="#FFF"/>
        </svg>
      </app-btn>
    </div>
  </div>
</template>

<script setup>
import {ref} from 'vue'
  const active = ref(false);
  const hh = ref("00");
  const min = ref("00");
  const seg = ref("00");
  const ms = ref("00");

    const startTimer = () => {
      active.value = !active.value
      setInterval(() => {
        if (active.value === true) {
          ms.value++;
          ms.value = ms.value < 10 ? "0" + ms.value : ms.value;

          if (ms.value === 100) {
            seg.value++;
            seg.value = seg.value < 10 ? "0" + seg.value : seg.value;

            ms.value = 0;
          }

          if (seg.value === 60) {
            min.value++;
            min.value = min.value < 10 ? "0" + min.value : min.value;

            seg.value = 0;
          }

          if (min.value === 60) {
            hh.value++;
            hh.value = hh.value < 10 ? "0" + hh.value : hh.value;

            min.value = 0;
          }
        }
      }, 10);
    }

    const stopTimer = () => {
      active.value = false;
      clearInterval(startTimer);
    };

    const restartTimer = () => {
      active.value = false;
      hh.value = "0"
      min.value = "0"
      seg.value = "0"
      ms.value = "0"
      clearInterval(startTimer);
    };
</script>
<style>
.card {
  padding: 20px 0;
  width: 225px;
  height: 120px;
  background: #696969;
  color: #FFFFFF;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.card__time {
  width: 100%;
  padding-bottom: 15px;
  border-bottom: 1px solid #fff;
  display: block;
  font-size: 22px;
}

.card__btns {
  margin-top: 20px;
  width: 82px;
  display: flex;
  justify-content: space-between;
}
</style>