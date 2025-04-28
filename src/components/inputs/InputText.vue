<template>
  <q-input
    :model-value="modelValue"
    @update:model-value="(val) => emits('update:modelValue', val)"
    class="input-rounded"
    :bg-color="$q.dark.isActive ? 'grey-10' : 'grey-2'"
    :readonly="readonly"
    outlined
    hide-bottom-space
    lazy-rules
    dense
    filled
  >
    <template v-if="modelValue && clearable && !readonly" v-slot:append>
      <q-icon
        class="cursor-pointer"
        name="close"
        @click.stop.prevent="emits('update:modelValue', null)"
      />
    </template>
  </q-input>
</template>

<script setup lang="ts">
defineOptions({
  name: 'InputText',
});

defineProps({
  modelValue: [String, Number],
  readonly: {
    type: Boolean,
    default: false,
  },
  clearable: {
    type: Boolean,
    default: true,
  },
});

const emits = defineEmits(['update:modelValue']);
</script>
