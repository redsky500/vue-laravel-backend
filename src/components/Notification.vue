<template>
    <div v-if="message" :class="['alert', alertClass]" role="alert">
      {{ message }}
    </div>
  </template>
  
  <script setup>
  import { defineProps, computed } from 'vue';
  
  const props = defineProps({
    message: String,
    type: {
      type: String,
      default: 'info',
    },
  });
  
  const alertClass = computed(() => `alert-${props.type}`);
  </script>
  