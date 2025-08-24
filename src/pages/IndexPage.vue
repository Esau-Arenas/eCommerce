<template>
  <q-page class="q-pa-md">
    <SearchHeader />
    <BannerCarousel />

    

    <div class="q-mt-xl">
      <h5>Recomendaciones</h5>
      <div class="row q-col-gutter-md q-mt-md">
        <ProductCard
          v-for="product in products"
          :key="product.id"
          :product="product"
          @add-to-cart="addToCart"
          @click="() => openDetails(product)" 
        />
      </div>
    </div>

    <q-dialog v-model="showDetails" persistent>
  <q-card style="min-width: 300px; max-width: 90vw;">
    
    <!-- Título del producto -->
    <q-card-section>
      <div class="text-h6">
        {{ selectedProduct?.title || 'Sin título' }}
      </div>
    </q-card-section>

    <!-- Imagen y detalles principales -->
    <q-card-section>
      <div v-if="selectedProduct?.image">
        <q-img :src="selectedProduct.image" style="max-height: 200px;" />
      </div>

      <div class="q-mt-sm text-subtitle1 text-negative">
        Precio: Q{{ selectedProduct?.price || 0 }}
      </div>
      <div v-if="selectedProduct?.discount">
        Descuento: {{ selectedProduct.discount }}%
      </div>
      <div v-if="selectedProduct?.opinions">
        Opiniones: {{ selectedProduct.opinions }}
      </div>
      <div v-if="selectedProduct?.description" class="q-mt-sm">
        <strong>Descripción:</strong> {{ selectedProduct.description }}
      </div>

      <!-- Metadatos del producto -->
      <div v-if="selectedProduct?.metadata" class="text-caption q-mt-xs">
        <div><strong>Origen:</strong> {{ selectedProduct.metadata.origin }}</div>
        <div><strong>Presentación:</strong> {{ selectedProduct.metadata.presentation }}</div>
        <div><strong>Producción:</strong> {{ selectedProduct.metadata.productionDate }}</div>
        <div><strong>Lote:</strong> {{ selectedProduct.metadata.batch }}</div>
      </div>
    </q-card-section>

    <!-- Acciones -->
    <q-card-actions align="right">
      <q-btn flat label="Cerrar" color="primary" v-close-popup />
      <q-btn
        flat
        label="Agregar al carrito"
        color="primary"
        @click="selectedProduct && addToCart(selectedProduct)"
      />
    </q-card-actions>
  </q-card>
</q-dialog>

  </q-page>

</template>

<script setup lang="ts">
import { ref } from 'vue'
import ProductCard from 'components/ProductCard.vue'
import BannerCarousel from 'components/BannerCarousel.vue'
import SearchHeader from 'components/SearchHeader.vue'
import { useCartStore } from 'stores/cart'


type Product = {
  id: number
  title: string
  price: number
  image: string
  discount?: number
  opinions?: number
  description?: string
  metadata?: {
    origin: string
    presentation: string
    productionDate: string
    batch: string
  }
}

const cart = useCartStore()

const products = ref<Product[]>([
  {
    id: 1,
    title: 'Café Soluble MayaCode – Clásico 100g',
    price: 55,
    image: 'https://images.unsplash.com/photo-1559056199-641a0ac8b55e?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    discount: 10,
    opinions: 24,
    description: 'Café soluble de alta calidad, aroma intenso y sabor suave. Ideal para preparar rápidamente una taza de café delicioso.',
    metadata: {
      origin: 'Guatemala',
      presentation: 'Tarro de vidrio 100g',
      productionDate: '2025-08-01',
      batch: 'MC-001'
    }
  },
  {
    id: 2,
    title: 'Café Soluble MayaCode – Intenso 100g',
    price: 60,
    image: 'https://images.unsplash.com/photo-1559056199-96c307526265?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    discount: 5,
    opinions: 18,
    description: 'Café soluble con sabor más fuerte y cuerpo completo. Perfecto para los amantes del café intenso.',
    metadata: {
      origin: 'Guatemala',
      presentation: 'Tarro de vidrio 100g',
      productionDate: '2025-08-05',
      batch: 'MC-002'
    }
  },
  {
    id: 3,
    title: 'Café Soluble MayaCode – Descafeinado 100g',
    price: 65,
    image: 'https://images.unsplash.com/photo-1633275513781-a04cf6d1454d?q=80&w=1232&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    discount: 0,
    opinions: 10,
    description: 'Café soluble descafeinado con el mismo sabor delicioso, ideal para disfrutar sin cafeína.',
    metadata: {
      origin: 'Guatemala',
      presentation: 'Tarro de vidrio 100g',
      productionDate: '2025-08-10',
      batch: 'MC-003'
    }
  },
  {
    id: 4,
    title: 'Café Soluble MayaCode – Mocha 100g',
    price: 70,
    image: 'https://images.unsplash.com/photo-1604497051809-896c56554ccd?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    discount: 15,
    opinions: 30,
    description: 'Café soluble con mezcla de chocolate, para un sabor único y exquisito. Ideal para los amantes del café con toque dulce.',
    metadata: {
      origin: 'Guatemala',
      presentation: 'Tarro de vidrio 100g',
      productionDate: '2025-08-12',
      batch: 'MC-004'
    }
  },
  {
    id: 5,
    title: 'Café Soluble MayaCode – Vainilla 100g',
    price: 72,
    image: 'https://images.unsplash.com/photo-1585702544354-406dcd2bf851?q=80&w=1169&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
    discount: 12,
    opinions: 22,
    description: 'Café soluble con esencia de vainilla, aroma envolvente y sabor delicado. Perfecto para disfrutar en cualquier momento.',
    metadata: {
      origin: 'Guatemala',
      presentation: 'Tarro de vidrio 100g',
      productionDate: '2025-08-15',
      batch: 'MC-005'
    }
  },
])

const selectedProduct = ref<Product | null>(null)
const showDetails = ref(false)

function openDetails(product: Product) {
  selectedProduct.value = product
  showDetails.value = true
}

function addToCart(product: Product) {
  cart.addItem(product)
}
</script>