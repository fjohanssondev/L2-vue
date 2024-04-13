<template>
  <section class="products">
    <div v-for="product in filteredProducts()">
      <ProductCard :key="product.id" v-bind="{product}" />
    </div>
  <p v-if="loading">Loading products...</p>
  </section>
</template>

<script setup lang="ts">
  import { ref } from "vue"
  import type { Product } from "../../../types/types"
  import ProductCard from "./ProductCard.vue"

  const props = defineProps({
    filterValue: {
      type: String,
      required: true
    }
  })

  const products = ref<Product[]>([])
  const loading = ref(true)

  const filteredProducts = () => props.filterValue !== "" ? products.value.filter(product => product.category === props.filterValue) : products.value
  const fetchProducts = async () => {
    loading.value = true
    
    try {
      const res = await fetch('https://fakestoreapi.com/products')
      
      if (res.ok){
        const articles = await res.json()
        products.value = articles
        loading.value = false
      }
    } catch(err){
      console.error(err)
    }
  }

  fetchProducts()
</script>

<style scoped lang="scss">
.products {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(16rem, 1fr));
  grid-auto-rows: 1fr;
  column-gap: 1rem;
  row-gap: 3rem;
}
</style>