<template>
  <div>
    <table class="contact-table">
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
          <th>Phone</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in contacts" :key="contact.id">
          <td>{{ contact.name }}</td>
          <td>{{ contact.email }}</td>
          <td>{{ contact.phone }}</td>
          <td>
            <button @click="editContact(contact)">
              <i class="fas fa-edit"></i>
            </button>
            <button @click="deleteContact(contact.id)">
              <i class="fas fa-trash"></i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from "vue";
import ContactForm from "../components/ContactForm.vue";
import Notification from "../components/Notification.vue";

const contacts = ref([]);
const currentContact = ref({ id: null, name: "", email: "", phone: "" });
const isEdit = ref(false);
const notification = ref({
  message: "",
  type: "info",
});

const saveContact = (contact) => {
  if (isEdit.value) {
    const index = contacts.value.findIndex((c) => c.id === contact.id);
    contacts.value.splice(index, 1, contact);
    showNotification("Contact updated successfully!", "success");
  } else {
    contact.id = Date.now();
    contacts.value.push(contact);
    showNotification("Contact added successfully!", "success");
  }
  resetForm();
};

const deleteContact = (id) => {
  contacts.value = contacts.value.filter((c) => c.id !== id);
  showNotification("Contact deleted successfully!", "danger");
};

const editContact = (contact) => {
  currentContact.value = { ...contact };
  isEdit.value = true;
};

const resetForm = () => {
  currentContact.value = { id: null, name: "", email: "", phone: "" };
  isEdit.value = false;
};

const showNotification = (message, type) => {
  notification.value = { message, type };
  setTimeout(() => {
    notification.value.message = "";
  }, 3000);
};
</script>

<style scoped>
.contact-table {
  width: 100%;
  border-collapse: collapse;
  margin: 20px 0;
}

.contact-table th,
.contact-table td {
  border: 1px solid #ddd;
  padding: 8px;
}

.contact-table th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #f2f2f2;
}

.contact-table td {
  text-align: center;
}

.contact-table button {
  background: none;
  border: none;
  cursor: pointer;
  padding: 5px;
}

.contact-table i {
  color: #007bff;
}

.contact-table i.fa-trash {
  color: #dc3545;
}

@media (max-width: 768px) {
  .contact-table {
    font-size: 0.9rem;
  }
}
</style>
