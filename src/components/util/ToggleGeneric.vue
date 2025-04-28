<template>
  <q-toggle
    :label="label"
    :model-value="modelValue"
    @update:model-value="(val) => emits('update:modelValue', val)"
  />
</template>

<script setup lang="ts">
defineOptions({
  name: 'ToggleGeneric',
});

defineProps({
  modelValue: Boolean,
  label: {
    type: String,
    required: true,
  },
});

const emits = defineEmits(['update:modelValue']);
</script>
