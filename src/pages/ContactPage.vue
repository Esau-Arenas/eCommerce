<template>
  <q-page class="q-pa-md">
    <h4>Formulario de Contacto</h4>
    <q-form @submit.prevent="submitForm" class="q-gutter-md">
      <q-input filled v-model="name" label="Nombre" required />
      <q-input filled v-model="email" label="Correo electrónico" type="email" required />
      <q-input filled v-model="message" label="Mensaje" type="textarea" required />
      <q-btn label="Enviar" color="primary" type="submit" />
    </q-form>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const name = ref('')
const email = ref('')
const message = ref('')

function submitForm() {
  alert(`Gracias ${name.value}, tu mensaje ha sido enviado!`)
  name.value = ''
  email.value = ''
  message.value = ''
}
</script>
