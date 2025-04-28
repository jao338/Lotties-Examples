<template>
  <q-slider
    :model-value="modelValue"
    @update:model-value="(val) => emits('update:modelValue', val)"
    :min="min"
    :max="max"
    :step="step"
  />
</template>

<script setup lang="ts">
defineOptions({
  name: 'SliderGeneric',
});

defineProps({
  modelValue: [String, Number],
  min: {
    type: Number,
    required: false,
    default: 0.1
  },
  max: {
    type: Number,
    required: false,
    default: 1
  },
  step: {
    type: Number,
    required: false,
    default: 0.1
  },
});

const emits = defineEmits(['update:modelValue']);

</script>
