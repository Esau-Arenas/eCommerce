<template>
  <q-page class="q-pa-md">
    <h4>Resumen de compra</h4>

    <div v-for="item in cart.items" :key="item.id" class="q-mb-sm">
      {{ item.title }} x {{ item.quantity }} - Q{{ item.price * item.quantity }}
    </div>

    <q-separator class="q-my-md" />

    <q-form @submit.prevent="finalizar">
      <div class="q-mb-md">
        <q-radio
          v-model="paymentMethod"
          val="tarjeta"
          label="Tarjeta de crédito/débito"
        />
        <q-radio
          v-model="paymentMethod"
          val="paypal"
          label="PayPal"
        />
        <q-radio
          v-model="paymentMethod"
          val="efectivo"
          label="Efectivo"
        />
      </div>

      <q-btn type="submit" label="Finalizar compra" color="green" />
    </q-form>

    <q-dialog v-model="showConfirmation">
      <q-card style="min-width: 300px; max-width: 400px;">
        <q-card-section class="text-h6">
          Pago realizado con éxito!
        </q-card-section>
        <q-card-section>
          <div>Método de pago: {{ paymentMethodLabel }}</div>
          <div>Total: Q{{ total }}</div>
        </q-card-section>
        <q-card-actions align="right">
          <q-btn flat label="Cerrar" color="primary" v-close-popup @click="showConfirmation = false" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { useCartStore } from 'stores/cart'

const cart = useCartStore()
const paymentMethod = ref('tarjeta')
const showConfirmation = ref(false)

const total = computed(() =>
  cart.items.reduce((acc, item) => acc + item.price * item.quantity, 0)
)

const paymentMethodLabel = computed(() => {
  switch (paymentMethod.value) {
    case 'tarjeta': return 'Tarjeta de crédito/débito'
    case 'paypal': return 'PayPal'
    case 'efectivo': return 'Efectivo'
    default: return ''
  }
})

function finalizar() {
  if (cart.items.length === 0) {
    alert('El carrito está vacío!')
    return
  }
  showConfirmation.value = true
  cart.clearCart()
}
</script>
