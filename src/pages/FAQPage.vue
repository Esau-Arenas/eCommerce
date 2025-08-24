<template>
  <q-page class="q-pa-md">
    <h4>Preguntas Frecuentes (FAQ)</h4>
    <q-expansion-item
      v-for="(faq, index) in faqs"
      :key="index"
      :label="faq.question"
      switch-toggle-side
    >
      <div>{{ faq.answer }}</div>
    </q-expansion-item>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const faqs = ref([
  {
    question: '¿Cómo puedo realizar una compra?',
    answer: 'Selecciona los productos que deseas, agrégalos al carrito y sigue al checkout para completar la compra.'
  },
  {
    question: '¿Puedo devolver un producto?',
    answer: 'Sí, puedes devolver productos dentro de los 15 días posteriores a la compra siguiendo nuestra política de devoluciones.'
  },
  {
    question: '¿Cuáles son los métodos de pago disponibles?',
    answer: 'Aceptamos tarjeta de crédito, débito y pagos simulados en nuestro entorno de prueba.'
  },
  {
    question: '¿Hacen envíos internacionales?',
    answer: 'Actualmente solo realizamos envíos dentro de Guatemala.'
  }
])
</script>
