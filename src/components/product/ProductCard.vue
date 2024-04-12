<template>
  <article class="product">
    <img class="product__image" :src="product.image" :alt="product.title" />
    <div class="product__content">
      <span class="product__category">{{ product.category.toUpperCase() }}</span>
      <h3 class="product__title">{{ product.title }}</h3>
      <p class="product__description">{{ product.description.slice(0, 100) }}</p>
    </div>
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

<style scoped lang="scss">
.product {
  display: flex;
  flex-direction: column;
  background-color: #f2f2f2;
  padding: 1rem;
  height: 100%;
  border-radius: 4px;

  &__content {
    margin-block: 1rem;
  }

  &__title {
    margin: 0;
  }

  &__category {
    font-size: 0.6rem;
    font-weight: 600;
  }

  &__image {
    width: 10rem;
    height: 12rem;
    margin-inline: auto;
  }

  &__description {
    margin-bottom: auto;
  }
}
</style>