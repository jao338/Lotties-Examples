<template>
  <Vue3Lottie
    ref="lottieRef"
    :animation-data="animationData"
    :height="height"
    :width="width"
    :loop="loop"
    :speed="speed"
    v-bind="animationLink"
    @onAnimationLoaded="isReady = true"
  />
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { type Vue3Lottie } from 'vue3-lottie';

defineOptions({
  name: 'LottieGeneric',
});

defineProps({
  animationData: {
    type: Object,
    required: true,
  },
  animationLink: {
    type: String,
    required: false,
    default: ''
  },
  height: {
    type: Number,
    default: 200,
  },
  width: {
    type: Number,
    default: 200,
  },
  loop: {
    type: [Boolean, Number],
    default: false,
  },
  speed: {
    type: Number,
    default: 1,
  },
});

const isReady = ref<boolean>(false);
const lottieRef = ref<InstanceType<typeof Vue3Lottie> | null>(null);

defineExpose({
  play: () => isReady.value && lottieRef.value?.play(),
  pause: () => isReady.value && lottieRef.value?.pause(),
  stop: () => isReady.value && lottieRef.value?.stop(),
  destroy: () => isReady.value && lottieRef.value?.destroy(),
  setDirection: (direction: 'forward' | 'reverse') => isReady.value && lottieRef.value?.setDirection(direction),
  getDuration: () => lottieRef.value?.getDuration()
});
</script>
