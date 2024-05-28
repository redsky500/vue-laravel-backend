<template>
  <div>
    <ContactForm :contact="contact" :isEdit="true" @submit="updateContact" />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";
import ContactForm from "../components/ContactForm.vue";

const route = useRoute();
const router = useRouter();
const contact = ref(null);

onMounted(() => {
  const contactId = Number(route.params.id);
  const parentContacts = route.meta.parentContacts; // Assuming parent contacts are passed through meta
  contact.value = parentContacts.find((c) => c.id === contactId);
});

const updateContact = (updatedContact) => {
  const parentContacts = route.meta.parentContacts; // Assuming parent contacts are passed through meta
  const index = parentContacts.findIndex((c) => c.id === updatedContact.id);
  parentContacts.splice(index, 1, updatedContact);
  router.push("/");
};
</script>
