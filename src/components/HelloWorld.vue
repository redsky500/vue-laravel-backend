<template>
  <div v-if="message" :class="['alert', alertClass]" role="alert">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: "Notification",
  props: {
    message: String,
    type: {
      type: String,
      default: "info",
    },
  },
  computed: {
    alertClass() {
      return `alert-${this.type}`;
    },
  },
};
</script>
