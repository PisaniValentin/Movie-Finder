<script setup lang="ts">
import TheHeader from './components/TheHeader.vue';
import TheBody from './components/TheBody.vue'
import Netflix from './components/Netflix.vue';
</script>

<template>
  <TheHeader />
  <TheBody>
    <template v-slot:netflix>
      <Netflix />
    </template>
    <template v-slot:disney>
      <Netflix />
    </template>
    <template v-slot:paramount>
      <Netflix />
    </template>
  </TheBody>
</template>
