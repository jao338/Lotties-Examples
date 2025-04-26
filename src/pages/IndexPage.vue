<template>
  <q-page class="row items-center justify-center">

    <q-card class="row justify-center items-center col-6">
      <q-card-section class="flex col-6">
        <Vue3Lottie ref="lottieRef" :animation-data="animation" :height="data.height" :width="data.width"
          :loop="data.loop" :speed="data.speed" />
      </q-card-section>
      <q-card-section class="row justify-start col-6 q-col-gutter-md">
        <q-checkbox v-model="data.loop" label="Loop" class="col-12" />
        <div class="col-12">
          <q-btn @click="play" label="Play" color="primary" />
          <q-btn @click="pause" label="Pause" color="primary" />
          <q-btn @click="stop" label="Stop" color="primary" />
          <q-toggle v-model="data.revert" label="Reverter" class="col-12" @update:model-value="revert" />
        </div>
        <span class="col-12">
          <p class="no-margin">Speed</p>
          <q-slider v-model="data.speed" :min="0.1" :max="3" :step="0.1" color="primary" />
        </span>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue'

import animation from 'src/assets/animations/checkbox.json'
interface Data {
  loop: boolean,
  speed: number,
  revert: boolean,
  width: number,
  height: number,
}

const data = ref<Data>({
  loop: true,
  speed: 1.0,
  revert: false,
  width: 200,
  height: 200,
})

const lottieRef = ref<any>(null)
function play(): void {
  lottieRef.value?.play()
}

function pause(): void {
  lottieRef.value?.pause()
}

function stop(): void {
  lottieRef.value?.stop()
}

/*************  ✨ Windsurf Command ⭐  *************/
/**
 * Revert the animation direction, if revert is true, the animation will be played
 * in reverse, if not, it will be played in forward.
 */
/*******  96b079e4-3436-40c8-9224-20ea87897fd9  *******/
function revert(): void {
  lottieRef.value?.setDirection(data.value.revert ? -1 : 1)
  lottieRef.value?.play()
}

</script>
