<script setup lang="ts">
import { nextTick } from 'process'
import { ref, onMounted } from 'vue'

const getDates = new Date()
const monthRef = ref(null)
const dayRef = ref(null)
const hoursRef = ref(null)
const minutesRef = ref(null)
const secondsRef = ref(null)
let year = getDates.getFullYear()
let month = getDates.getMonth() + 1
let day = getDates.getDate()
let hours = getDates.getHours()
let minutes = getDates.getMinutes()
let seconds = getDates.getSeconds()
const days = new Date(year, month, 0).getDate()

onMounted(() => {
  revolveFun()
})

const revolve = () => {}

const revolveFun = () => {
  monthRef.value.style.transform = `rotate(${month * 30}deg)`
  dayRef.value.style.transform = `rotate(${day * (360 / days)}deg)`
  hoursRef.value.style.transform = `rotate(${hours * 15}deg)`
  minutesRef.value.style.transform = `rotate(${minutes * 6}deg)`
  secondsRef.value.style.transform = `rotate(${(seconds - 1) * 6}deg)`
  setInterval(() => {
    const getDates = new Date()
    let newSeconds = getDates.getSeconds()
    let newMinutes = getDates.getMinutes()
    let newHours = getDates.getHours()
    seconds++
    secondsRef.value.style.transform = `rotate(${(seconds - 1) * 6}deg)`
    console.log('秒：', newSeconds)
    console.log('分：', newMinutes)
    console.log('时：', newHours)
    if (newSeconds == 0) {
      minutes = minutes + 1
      minutesRef.value.style.transform = `rotate(${minutes * 6}deg)`
    }
    if (newMinutes == 0) {
      hours++
      hoursRef.value.style.transform = `rotate(${hours * 15}deg)`
    }
    if (newHours == 0) {
      day++
      dayRef.value.style.transform = `rotate(${day * (360 / days)}deg)`
    }
  }, 1000)
}
</script>

<template>
  <div class="outer_layer">
    <div class="year">{{ year }}年</div>
    <div class="month" ref="monthRef">
      <div
        v-for="item in 12"
        :key="item"
        :style="{
          transform: 'rotate(' + item * -30 + 'deg)'
        }"
      >
        {{ item }} 月
      </div>
    </div>
    <div class="month2" ref="dayRef">
      <div
        v-for="item in days"
        :key="item"
        :style="{
          transform: 'rotate(' + item * -(360 / days) + 'deg)'
        }"
      >
        {{ item }} 日
      </div>
    </div>
    <div class="month3" ref="hoursRef">
      <div
        v-for="item in 24"
        :key="item"
        :style="{
          transform: 'rotate(' + item * -15 + 'deg)'
        }"
      >
        {{ item }} 时
      </div>
    </div>
    <div class="month4" ref="minutesRef">
      <div
        v-for="item in 60"
        :key="item"
        :style="{
          transform: 'rotate(' + item * -6 + 'deg)'
        }"
      >
        {{ item }} 分
      </div>
    </div>
    <div class="month5" ref="secondsRef">
      <div
        v-for="item in 60"
        :key="item"
        :style="{
          transform: 'rotate(' + (item - 1) * -6 + 'deg)'
        }"
      >
        {{ item }} 秒
      </div>
    </div>
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}
body {
  width: 100%;
  height: 100%;
}
.outer_layer {
  width: 100%;
  height: 100%;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #cad6dd;
  overflow: hidden;
  font-size: 18px;
  .year {
    position: absolute;
    width: 10vh;
    text-align: center;
    font-size: 20px;
  }
  .month,
  .month2,
  .month3,
  .month4,
  .month5 {
    width: 20vh;
    height: 20vh;
    position: absolute;
    display: flex;
    align-items: center;
    transition: 0.9s;
    div {
      width: 100%;
      text-align: right;
      display: inline-block;
      position: absolute;
    }
  }
  .month {
  }
  .month2 {
    width: 38vh;
    height: 38vh;
  }
  .month3 {
    width: 56vh;
    height: 56vh;
  }
  .month4 {
    width: 74vh;
    height: 74vh;
  }
  .month5 {
    width: 92vh;
    height: 92vh;
  }
}
</style>
