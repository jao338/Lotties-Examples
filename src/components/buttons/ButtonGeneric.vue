<template>
  <q-btn color="primary" class="q-border-radius" :label="label" />
</template>

<script setup lang="ts">
import { type ButtonGeneric } from 'src/components/Interface'

withDefaults(defineProps<ButtonGeneric>(), {
  label: '',
})
</script>
