<template>
    <div>
      <h3>Contacts List</h3>
      <ul class="list-group">
        <li v-for="contact in contacts" :key="contact.id" class="list-group-item">
          <ContactItem :contact="contact" @delete="deleteContact" @edit="editContact" />
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  import ContactItem from './ContactItem.vue';
  
  const props = defineProps(['contacts']);
  const emit = defineEmits(['delete', 'edit']);
  
  const deleteContact = (id) => {
    emit('delete', id);
  };
  
  const editContact = (contact) => {
    emit('edit', contact);
  };
  </script>
  