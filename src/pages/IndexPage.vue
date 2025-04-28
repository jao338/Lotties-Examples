<template>
  <q-page class="row items-center justify-center">
    <q-card class="row justify-center items-center col-lg-6 col-md-8 col-sm-8 col-xs-8">
      <q-card-section class="row justify-start q-col-gutter-md col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12">
        <p class="col-12 text-h6">{{ $t("animation") }}</p>
        <Vue3Lottie class="col-12 rounded-borders" ref="lottieRef" :animation-data="animation" :height="data.height"
          :width="data.width" :loop="data.loop" :speed="data.speed" @onComplete="handleComplete"
          @onLoopComplete="handleLoopComplete" @onAnimationLoaded="getInfo" />
      </q-card-section>
      <q-card-section class="row justify-start col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12 q-col-gutter-md">
        <p class="col-12 text-h6">{{ $t("controllers") }}</p>
        <div class="col-12 row q-col-gutter-md">
          <div class="flex q-gutter-md col-12">
            <q-checkbox v-model="data.loop" :label="$t('loop')" class="col-12" />
            <q-toggle v-model="data.revert" :label="$t('revert')" class="col-12" @update:model-value="revert" />
          </div>
          <div class="flex q-gutter-md col-12">
            <q-btn @click="play" :label="$t('play')" color="primary" />
            <q-btn @click="pause" :label="$t('pause')" color="primary" />
            <q-btn @click="stop" :label="$t('stop')" color="primary" />
            <q-btn @click="destroy" :label="$t('destroy')" color="primary" />
          </div>
          <div class="col-12 q-gutter-md">
            <p class="text-caption">{{ $t("size") }}</p>
            <q-input v-model="data.width" type="number" :label="$t('width')" dense filled />
            <q-input v-model="data.height" type="number" :label="$t('height')" dense filled />
          </div>
          <span class="col-12">
            <p class="no-margin text-caption">{{ $t("speed") }}</p>
            <q-slider v-model="data.speed" :min="0.1" :max="2" :step="0.1" color="primary" />
          </span>
        </div>
      </q-card-section>
    </q-card>

    <div class="row justify-center items-center col-lg-8 col-md-8 col-sm-8 col-xs-8">
      <q-card class="row justify-center items-center col-xl-9 col-lg-9 col-md-12 col-sm-12 col-xs-12">
        <p class="text-h6 text-center q-mt-md col-12">{{ $t("info") }}</p>
        <p v-if="animationHasLoaded" class="text-caption col-12 text-center">{{ $t("loadAnimation") }}</p>
        <p v-if="animationHasEnded" class="text-caption col-12 text-center">{{ $t("endedAnimation") }}</p>
        <p class="text-caption col-12 text-center">
          {{ $t("durationInfo") }}:
          <span class="text-bold">{{ duration }} {{ $t("frames") }}</span>
        </p>
        <p class="text-caption col-12 text-center">
          {{ $t("width") }}: <span class="text-bold">{{ data.width }}px</span>
        </p>
        <p class="text-caption col-12 text-center">
          {{ $t("height") }}: <span class="text-bold">{{ data.height }}px</span>
        </p>
      </q-card>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { type Vue3Lottie } from 'vue3-lottie';

import animation from 'src/assets/animations/checkbox.json';
interface Data {
  loop: boolean;
  speed: number;
  revert: boolean;
  width: number;
  height: number;
}

const data = ref<Data>({
  loop: true,
  speed: 1.0,
  revert: false,
  width: 200,
  height: 200,
});

const duration = ref<number>(0);
const animationHasLoaded = ref<boolean>(false);
const animationHasEnded = ref<boolean>(false);
const numberOfLoops = ref<number>(0);

const lottieRef = ref<InstanceType<typeof Vue3Lottie> | null>(null);
function play(): void {
  lottieRef.value?.play();
}

function pause(): void {
  lottieRef.value?.pause();
}

function stop(): void {
  lottieRef.value?.stop();
}

function destroy(): void {
  lottieRef.value?.destroy();
}

function revert(): void {
  const direction = data.value.revert ? 'reverse' : 'forward';
  lottieRef.value?.setDirection(direction);
  setTimeout(() => lottieRef.value?.play(), 100);
}

function handleLoopComplete(): void {
  console.log('Um loop da animação foi concluído!');
}

function handleComplete(): void {
  animationHasEnded.value = true;
}

//  This function will be executed when the animation is ready
function getInfo(): void {
  play();
  animationHasLoaded.value = true;
  duration.value = lottieRef.value?.getDuration() || 0;
}

</script>
