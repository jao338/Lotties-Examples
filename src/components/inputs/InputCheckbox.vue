<template>
  <q-checkbox
    :label="label"
    :model-value="modelValue"
    @update:model-value="(val) => emits('update:modelValue', val)"
    :disable="readonly"
    dense
  />
</template>

<script setup lang="ts">
defineOptions({
  name: 'InputCheckbox',
});

defineProps({
  modelValue: [String, Boolean, Number],
  label: {
    type: String,
    required: true,
  },
  readonly: {
    type: Boolean,
    default: false,
  },
});

const emits = defineEmits(['update:modelValue']);
</script>
