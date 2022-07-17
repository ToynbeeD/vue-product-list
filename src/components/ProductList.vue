<template>
  <ul class="list">
    <ProductItem class="list__item" v-for="product in productAmount" :key="product" />
  </ul>
</template>

<script>
import ProductItem from '@/components/ProductItem.vue'
export default {
  components: { ProductItem },
  props: {
    productAmount: Number
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';
@import '@/assets/scss/mixins.scss';

.list {
  @include flex(flex-start);
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
