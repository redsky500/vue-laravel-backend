<template>
  <div v-if="contact">
    <h3>{{ contact.name }}</h3>
    <p>Email: {{ contact.email }}</p>
    <p>Phone: {{ contact.phone }}</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();
const contact = ref(null);

onMounted(() => {
  const contactId = Number(route.params.id);
  const parentContacts = route.meta.parentContacts; // Assuming parent contacts are passed through meta
  contact.value = parentContacts.find((c) => c.id === contactId);
});
</script>
