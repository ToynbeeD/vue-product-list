<template>
  <ul class="list">
    <ProductItem
      class="list__item"
      v-for="product in productsList"
      :key="product.id"
      :product="product"
      @deleteProduct="deleteProduct"
    />
  </ul>
</template>

<script>
import ProductItem from '@/components/ProductItem.vue'
export default {
  components: { ProductItem },
  props: {
    productsList: Array
  },
  methods: {
    deleteProduct (product) {
      this.$emit('deleteProduct', product)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';
@import '@/assets/scss/mixins.scss';

.list {
  display: flex;
  flex-wrap: wrap;

  &__item {
    margin-bottom: 16px;
    flex: 0 1 332px;

    &:not(:nth-child(3n)) {
      margin-right: 16px;
    }
  }
}
</style>
