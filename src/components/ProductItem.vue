<template>
  <li class="item">
    <button class="item__delete" @click="deleteProduct">
      <svg>
        <use xlink:href="@/assets/img/icons.svg#delete"></use>
      </svg>
    </button>
    <div class="item__image">
      <img class="item__image-content" :src="product.imageSrc" :alt="capitalizeProductName">
    </div>
    <div class="item__content">
      <h2 class="item__content-heading"> {{ capitalizeProductName }} </h2>
      <p class="item__content-description"> {{ product.description }} </p>
      <span class="item__content-price"> {{ formatPrice }} руб. </span>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    product: Object
  },
  methods: {
    deleteProduct () {
      this.$emit('deleteProduct', this.product)
    }
  },
  computed: {
    formatPrice () {
      return new Intl.NumberFormat().format(this.product.price)
    },
    capitalizeProductName () {
      return this.product.name[0].toUpperCase() + this.product.name.slice(1)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';
@import '@/assets/scss/mixins.scss';

.item {
  position: relative;
  border-radius: 4px;
  box-shadow: $shadowSmall;

  &__delete {
    @include flex(center);
    @include size(32px, 32px);
    @include transition(opacity);
    position: absolute;
    right: -8px;
    top: -8px;
    justify-content: center;
    background-color: $deleteColor;
    border-radius: 10px;
    cursor: pointer;
    opacity: 0;

    svg {
      @include size(16px, 16px);
      fill: $white
    }
  }

  &:hover &__delete {
    opacity: 1;
  }

  &__image {
    @include size(100%, 200px);
    border-top-right-radius: 4px;
    border-top-left-radius: 4px;
    overflow: hidden;

    &-content {
      @include size(100%, 100%);
      object-fit: cover;
    }
  }

  &__content {
    @include flex(flex-start);
    height: calc(100% - 200px);
    flex-direction: column;
    padding: 16px;
    padding-bottom: 24px;

    &-heading {
      @include fontOptions(20px, 120%);
      margin-bottom: 16px;
    }

    &-description {
      @include fontOptions(16px, 20px);
      margin-bottom: auto;
    }

    &-price {
      @include fontOptions(24px, 100%);
      display: block;
      margin-top: 32px;
      font-weight: 600;
    }
  }
}
</style>
