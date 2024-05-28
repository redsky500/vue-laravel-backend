<template>
    <div class="d-flex justify-content-between align-items-center">
      <div>
        <h5>{{ contact.name }}</h5>
        <p>{{ contact.email }} | {{ contact.phone }}</p>
      </div>
      <div>
        <button class="btn btn-secondary me-2" @click="editContact">Edit</button>
        <button class="btn btn-danger" @click="deleteContact">Delete</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  
  const props = defineProps(['contact']);
  const emit = defineEmits(['delete', 'edit']);
  
  const deleteContact = () => {
    emit('delete', props.contact.id);
  };
  
  const editContact = () => {
    emit('edit', props.contact);
  };
  </script>
  