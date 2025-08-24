<template>
  <q-header elevated class="bg-red-600 text-white">
    <q-toolbar>
      <!-- iconos y logo -->
      <q-toolbar-title>
        <span class="q-ml-sm">MAYA CODE</span>
      </q-toolbar-title>

      <!-- input de búsqueda -->
      <q-input
        rounded
        dense
        filled
        debounce="300"
        class="bg-white text-black"
        placeholder="Buscar en la tienda"
        v-model="search"
      >
        <template #append>
          <q-icon name="search" />
        </template>
      </q-input>

      <q-btn flat round dense icon="favorite_border" />
      <q-btn flat round dense icon="person" />
      <q-btn flat round dense @click="isDrawerOpen = true" icon="shopping_cart">
      <q-badge
        v-if="cart.items.length"
        color="red"
        floating
        transparent
        :label="cart.items.length"
      />
</q-btn>
    </q-toolbar>

    <!-- Drawer del carrito -->
    <CartDrawer v-model:isOpen="isDrawerOpen" />
  </q-header>
</template>

<script setup lang="ts">
import CartDrawer from 'components/CartDrawer.vue'
import { ref } from 'vue'
import { useCartStore } from 'stores/cart'

const search = ref('')
const isDrawerOpen = ref(false)
const cart = useCartStore()

</script>
