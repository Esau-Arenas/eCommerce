<template>
  <q-page class="q-pa-md">
    <h4>Resumen de compra</h4>
    <div v-for="item in cart.items" :key="item.id">
      {{ item.title }} x {{ item.quantity }} - ${{ item.price * item.quantity }}
    </div>
    <q-separator class="q-my-md" />
    <q-btn label="Finalizar compra" color="green" @click="finalizar" />
  </q-page>
</template>

<script setup lang="ts">
import { useCartStore } from 'stores/cart'
const cart = useCartStore()

function finalizar() {
  alert('Compra completada!')
  cart.clearCart()
}
</script>