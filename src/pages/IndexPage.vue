<template>
  <PageGeneric class="row items-center justify-center q-gutter-lg">
    <CardGeneric class="row justify-center items-between col-xl-6 col-lg-6 col-md-8 col-sm-10 col-xs-10">

      <template v-slot:left>
        <p class="col-12 text-h6">{{ $t('animation') }}</p>
        <LottieGeneric
          class="col-10"
          ref="lottieRef"
          :animation-data="animation"
          :height="data.height"
          :width="data.width"
          :loop="data.loop"
          :speed="data.speed"
          @onComplete="animationHasEnded.value = true"
          @onLoopComplete="handleLoopComplete"
          @onAnimationLoaded="getInfo"
        />
      </template>
      <template v-slot:right>
        <p class="col-12 text-h6">{{ $t('controllers') }}</p>
        <div class="col-12 row q-col-gutter-md">
          <div class="flex q-gutter-md col-12">
            <InputCheckbox
              v-model="data.loop"
              :label="$t('loop')"
              class="col-12"
            />
            <ToggleGeneric
              v-model="data.revert"
              :label="$t('revert')"
              class="col-12"
              @click="revert"
            />
          </div>
          <div class="flex items-center q-gutter-md col-12">
            <ButtonGeneric @click="lottieRef?.play" :label="$t('play')"/>
            <ButtonGeneric @click="lottieRef?.pause" :label="$t('pause')"/>
            <ButtonGeneric @click="lottieRef?.stop" :label="$t('stop')"/>
            <ButtonGeneric @click="lottieRef?.destroy" :label="$t('destroy')"/>
          </div>
          <div class="col-12 q-gutter-md">
            <p class="text-caption">{{ $t('size') }}</p>
            <InputText
              v-model="data.width"
              type="number"
              :label="$t('width')"
            />
            <InputText
              v-model="data.height"
              type="number"
              :label="$t('height')"
            />
          </div>
          <span class="col-12">
            <p class="no-margin text-caption">{{ $t('speed') }}</p>
            <SliderGeneric
              v-model="data.speed"
              :min="0.1"
              :step="0.1"
              :max="2"
              color="primary"
            />
          </span>
        </div>
      </template>

    </CardGeneric>
    <div class="row col-xl-6 col-lg-6 col-md-8 col-sm-10 col-xs-10">
      <CardGeneric class="row justify-center items-between col-xl-12 col-lg-12 col-md-12 col-sm-12 col-xs-12">

        <template v-slot:left>
          <p class="text-h6 col-12">{{ $t('animationInfo') }}</p>
          <div class="col-12">
            <p v-if="animationHasLoaded" class="text-caption q-my-sm">
              {{ $t('loadAnimation') }}
            </p>
            <p v-if="animationHasEnded" class="text-caption q-my-sm">
              {{ $t('endedAnimation') }}
            </p>
            <p class="text-caption q-my-sm">
              {{ $t('durationInfo') }}:
              <span class="text-bold">{{ duration }} {{ $t('frames') }}</span>
            </p>
            <p class="text-caption q-my-sm">
              {{ $t('numberOfLoops') }}:
              <span class="text-bold">{{ numberOfLoops }}</span>
            </p>
            <p class="text-caption q-my-sm">
              {{ $t('width') }}: <span class="text-bold">{{ data.width }}px</span>
            </p>
            <p class="text-caption q-my-sm">
              {{ $t('height') }}:
              <span class="text-bold">{{ data.height }}px</span>
            </p>
          </div>
        </template>
        <template v-slot:right>
          <p class="text-h6 col-12">{{ $t('lottieInfo') }}</p>
          <div class="row col-12">
            <ul class="col-10 q-pa-none">
              <li>{{ $t('lottieInfo1') }}</li>
              <li>{{ $t('lottieInfo2') }}</li>
              <li>{{ $t('lottieInfo3') }}</li>
              <li>{{ $t('lottieInfo4') }}</li>
            </ul>
          </div>
        </template>

      </CardGeneric>
    </div>
  </PageGeneric>
</template>

<script setup lang="ts">
import { ref } from 'vue';

import animation from 'src/assets/animations/checkbox.json';
import ButtonGeneric from 'src/components/buttons/ButtonGeneric.vue';
import CardGeneric from 'components/cards/CardGeneric.vue';
import PageGeneric from 'components/util/PageGeneric.vue';
import InputCheckbox from 'components/inputs/InputCheckbox.vue';
import InputText from 'components/inputs/InputText.vue';
import SliderGeneric from 'components/util/SliderGeneric.vue';
import ToggleGeneric from 'components/util/ToggleGeneric.vue';
import LottieGeneric from 'components/util/LottieGeneric.vue';

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

const lottieRef = ref<InstanceType<typeof LottieGeneric> | null>(null);

function revert(): void {
  lottieRef.value.setDirection(data.value.revert ? 'reverse' : 'forward');
  setTimeout(() => lottieRef.value.play(), 500);
}

function handleLoopComplete(): void {
  numberOfLoops.value++;
}

//  This function will be executed when the animation is ready
function getInfo(): void {
  lottieRef.value.play();
  animationHasLoaded.value = true;
  duration.value = lottieRef.value.getDuration();
}
</script>
