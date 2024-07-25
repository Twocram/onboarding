<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'
import confetti from './assets/confetti.gif'
import onB1 from './assets/onB-1.png'
import onB2 from './assets/onB-2.png'
import onB31 from './assets/onB-31.png'
import onB32 from './assets/onB-32.png'
import stars from './assets/star.gif'
import VButton from './components/VButton.vue'

const emits = defineEmits(['closeBoard']);

const activeSlide = ref<number>(1);

function nextSlide() {
  activeSlide.value++;
  if (activeSlide.value === 4) {
    emits('closeBoard');
  }
}
function prevSlide() {
  if (activeSlide.value === 2 || activeSlide.value === 3) {
    activeSlide.value--;
  }
}
function skipSlides() {
  emits('closeBoard');
}

const onboarding = localStorage.getItem('onboarding');

if (onboarding === null) {
  // localStorage.setItem('onboarding', 'true');
} else {
  // activeSlide.value = 4;
}


let startX: number | undefined;

addEventListener('touchstart', (e) => {
  startX = e.changedTouches[0]?.clientX;
});

addEventListener('touchend', (e) => {
  if (startX) {
    const endX = e.changedTouches[0]?.clientX;
    if (endX) {
      const swipeDistance = endX - startX;

      if (swipeDistance > 50) {
        swipeRight();
      } else if (swipeDistance < -50) {
        swipeLeft();
      }
    }
  }
});

function swipeLeft() {
  nextSlide();
}

function swipeRight() {
  prevSlide();
}


const isBigWidth = computed(() => {
  return window.innerWidth > 450;
});

const isSmallHeight = computed(() => {
  return window.innerHeight < 650;
});

onMounted(() => {
  document.body.classList.add('overflow');
});

onBeforeUnmount(() => {
  document.body.classList.remove('overflow');
});
</script>

<template>
  <div class="boarding-wrapper">
    <div class="lines">
      <div v-if="activeSlide > 0" class="line" />
      <div v-if="activeSlide > 1" class="line" />
      <div v-if="activeSlide > 2" class="line" />
      <div v-if="activeSlide < 2" class="line-inactive line" />
      <div v-if="activeSlide < 3" class="line-inactive line" />
    </div>
    <div
      :class="[{ showScreen: activeSlide === 1 }, { hidden: activeSlide !== 1 }]"
      class="boarding-screen boarding-screen_first">
      <img class="img1" :class="{ small: isSmallHeight }" :src="onB1" alt="" srcset="" />
      <div>
        <div class="head head_1">Premium kicks, smarter price</div>
        <div class="description">
          Dive into raffles where everyone has a shot at winning big. It's about making top-tier
          sneakers accessible — because everyone deserves that winning feeling.
        </div>
        <VButton color="wight" class="btn-1" @click="nextSlide"> Next </VButton>
        <div class="skip-text" @click="skipSlides">Skip</div>
      </div>
    </div>
    <div
      :class="[{ showScreen: activeSlide === 2 }, { hidden: activeSlide !== 2 }]"
      class="boarding-screen boarding-screen_second">
      <img
        class="img2"
        :class="[{ big: isBigWidth }, { small: isSmallHeight }]"
        :src="onB2"
        alt=""
        srcset="" />
      <div>
        <div class="head">Fair play</div>
        <div class="description second">
          Fairness first with a trusted random number picker, and full transparency in displaying
          entries and winners.
        </div>
        <VButton color="wight" class="btn-2" @click="nextSlide"> Next </VButton>
      </div>
    </div>
    <div
      :class="[{ showScreen: activeSlide === 3 }, { hidden: activeSlide !== 3 }]"
      class="boarding-screen boarding-screen_third">
      <div class="img-container">
        <img
          class="img3"
          :class="[{ big: isBigWidth }, { small: isSmallHeight }]"
          :src="onB31"
          alt=""
          srcset="" />
        <img
          class="img4"
          :class="[{ big: isBigWidth }, { small: isSmallHeight }]"
          :src="onB32"
          alt=""
          srcset="" />
        <img
          class="stars"
          :class="[{ big: isBigWidth }, { small: isSmallHeight }]"
          :src="stars"
          alt=""
          srcset="" />
        <img
          class="confetti"
          :class="[{ big: isBigWidth }, { small: isSmallHeight }]"
          :src="confetti"
          alt=""
          srcset="" />
      </div>
      <div>
        <div class="head">Clear win</div>
        <div class="description">
          Prize delivery to the winner is confirmed either with a DHL AWB or a USDT transaction ID.
        </div>
        <VButton color="wight" class="btn-3" @click="nextSlide"> Next </VButton>
      </div>
    </div>
  </div>
</template>

<style scoped>
.boarding-wrapper {
  position: relative;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 100;
  width: 100%;
}

.head {
  font-size: 11.02vw;
  font-weight: 600;
  line-height: 12.13vw;
  color: white;
  text-align: center;
}

.boarding-screen {
  visibility: visible;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  height: 100dvh;
  padding: 13.12vw 6.56vw 6.3vw;
  background-size: cover;
}

.description {
  margin: 3.15vw auto 4.3vw;
  font-size: 4.2vw;
  font-weight: 500;
  line-height: 5.88vw;
  color: white;
  text-align: center;
}

.description.second {
  margin: 3.15vw auto 3.3vw;
}

img {
  width: 100%;
}

.skip-text {
  margin-top: 3.25vw;
  font-size: 16px;
  font-weight: 500;
  line-height: 5.88vw;
  color: white;
  text-align: center;
  cursor: pointer;
}

.img-container {
  position: relative;
  width: 78.74vw;
  height: 78.74vw;
  padding-top: 10dvh;
  margin-bottom: auto;
  margin-top: auto;
}

.img-container.big {
  padding-top: 0;
}

.confetti {
  position: absolute;
  top: 8.62dvh;
  left: 38.06dvw;
  z-index: 2;
  width: 35.23dvw;
}

.confetti.small {
  position: absolute;
  top: 4.62dvh;
  left: 38.06dvw;
  z-index: 2;
  width: 31.23dvw;
}

.confetti.big {
  top: -2.62dvh;
}

.confetti.small {
  top: -2.62dvh;
}

.stars {
  position: absolute;
  bottom: -3.07dvh;
  left: -7.87dvw;
  z-index: 2;
  width: 23.13dvw;
  transform: rotate(6.89 deg);
}

.stars.small {
  position: absolute;
  bottom: 5.07dvh;
  left: -7.87dvw;
  z-index: 2;
  width: 19.13dvw;
  transform: rotate(6.89 deg);
}

.stars.big {
  bottom: 12.02dvh;
}

.start.small {
  bottom: 12.02dvh;
}

.img3.small,
.img4.small {
  position: absolute;
  width: 43.04dvw;
  border-radius: 12px;
}

.img3,
.img4 {
  position: absolute;
  width: 52.04dvw;
  border-radius: 12px;
}

.img4 {
  top: 3vh;
  left: 0;
  z-index: 1;
}

.img4.small {
  top: 3vh;
  left: 0;
  z-index: 1;
}

.img3 {
  right: 0;
  bottom: -14vh;
  right: -3vw;
  z-index: 3;
  box-shadow: 0 0 16px 0 #8f8f8f;
}

.img3.small {
  right: 0;
  bottom: -3vh;
  z-index: 3;
  box-shadow: 0 0 16px 0 #8f8f8f;
}

.img3.big {
  bottom: 0;
}

.img3.small {
  bottom: 0;
}

.img4.big {
  top: 0;
}

.img4.small {
  top: 0;
}

.boarding-screen.hidden {
  visibility: hidden;
}

.boarding-screen_first {
  padding-top: 10vw;
  background-image: url('./assets/onB-bg1.png');
}

.boarding-screen_second {
  background-image: url('./assets/onB-bg2.png');
}

.boarding-screen_third {
  background-image: url('./assets/onB-bg3.png');
}

.showScreen {
  z-index: 2;
}

.line {
  width: 48px;
  height: 4px;
  background-color: white;
  border-radius: 500px;
}

.line-inactive {
  background-color: #ffffff29;
}

.lines {
  position: fixed;
  top: 6.3vw;
  left: 50%;
  z-index: 3;
  display: flex;
  gap: 6px;
  transform: translateX(-50%);
}

.btn-2 {
  color: var(--color-orange);
}

.btn-3 {
  color: var(--color-red);
}

.img1 {
  margin-top: auto;
  margin-bottom: auto;
}

.img1.small {
  width: 90%;
}

.img1 {
  width: 120%;
}

.img2 {
  width: 110%;
  margin-top: auto;
  margin-bottom: auto;
}

.img2.small {
  width: 85%;
}

.head_1 {
  margin-top: -7vw;
}
</style>
