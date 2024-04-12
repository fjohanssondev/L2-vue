<template>
  <section>
    <div v-for="product in products">
      <ProductCard :key="product.id" v-bind="{product}" />
    </div>
  <p v-if="loading">Loading products...</p>
  </section>
</template>

<script setup lang="ts">
  import { ref } from "vue"
  import type { Product } from "../../../types/types"
  import ProductCard from "./ProductCard.vue"

  const products = ref<Product[]>([])
  const loading = ref(true)

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

<style scoped>

</style>