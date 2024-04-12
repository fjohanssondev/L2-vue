<template>
  <article>
    <img :src="product.image" :alt="product.title" />
    <span>{{ product.category.toUpperCase() }}</span>
    <h3>{{ product.title }}</h3>
    <p>{{ product.description }}</p>
  </article>
</template>

<script setup lang="ts">
  import type { Product } from "../../../types/types"

  defineProps({
    product: {
      type: Object as () => Product,
      required: true
    }
  })
</script>

<style scoped>

</style>