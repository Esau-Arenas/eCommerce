<template>
  <q-page class="q-pa-md">
    <SearchHeader />
    <BannerCarousel />

    <div class="q-mt-lg">
      <CategoryList />
    </div>

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
        <q-card-section>
          <div class="text-h6">
            {{ selectedProduct?.title || 'Sin título' }}
          </div>
        </q-card-section>

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
        </q-card-section>

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
import CategoryList from 'components/CategoryList.vue'
import SearchHeader from 'components/SearchHeader.vue'
import { useCartStore } from 'stores/cart'


type Product = {
  id: number
  title: string
  price: number
  image: string
  discount?: number
  opinions?: number
}

const cart = useCartStore()

const products = ref<Product[]>([
  {
    id: 1,
    title: 'Samsung Galaxy S24',
    price: 8199,
    image: 'https://i0.wp.com/phonexgt.com/wp-content/uploads/2024/01/22.jpg?fit=600%2C600&ssl=1',
    discount: 34,
    opinions: 12,
  },
  {
    id: 2,
    title: 'Samsung Galaxy J12',
    price: 4100,
    image: 'https://miro.medium.com/v2/resize:fit:668/0*kh1iRZ-uri1d6S2J.jpg',
    discount: 34,
    opinions: 12,
  },
  // puedes agregar más productos
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