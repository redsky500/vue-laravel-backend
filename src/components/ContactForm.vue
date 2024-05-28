<template>
    <div>
      <h3>{{ isEdit ? 'Edit' : 'Add' }} Contact</h3>
      <form @submit.prevent="handleSubmit">
        <div class="mb-3">
          <label for="name" class="form-label">Name</label>
          <input type="text" class="form-control" v-model="localContact.name" required />
        </div>
        <div class="mb-3">
          <label for="email" class="form-label">Email</label>
          <input type="email" class="form-control" v-model="localContact.email" required />
        </div>
        <div class="mb-3">
          <label for="phone" class="form-label">Phone</label>
          <input type="text" class="form-control" v-model="localContact.phone" required />
        </div>
        <button type="submit" class="btn btn-primary">{{ isEdit ? 'Update' : 'Add' }}</button>
      </form>
    </div>
  </template>
  
  <script setup>
  import { ref, watch, defineProps, defineEmits } from 'vue';
  
  const props = defineProps(['contact', 'isEdit']);
  const emit = defineEmits(['submit']);
  
  const localContact = ref({ ...props.contact });
  
  watch(() => props.contact, (newContact) => {
    localContact.value = { ...newContact };
  });
  
  const handleSubmit = () => {
    emit('submit', { ...localContact.value });
  };
  </script>
  