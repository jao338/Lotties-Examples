<template>
  <q-card class="q-pt-lg">
    <q-card-section class="row justify-start col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12 q-col-gutter-md">
      <slot name="left"/>
    </q-card-section>
    <q-card-section class="row justify-start col-xl-6 col-lg-6 col-md-6 col-sm-12 col-xs-12 q-col-gutter-md">
      <slot name="right"/>
    </q-card-section>
  </q-card>
</template>

<script setup lang="ts"></script>
