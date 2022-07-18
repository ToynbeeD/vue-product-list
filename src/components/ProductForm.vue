<template>
  <form class="form" action="#" @submit.prevent="addProduct">
    <label class="form__label">
      <span class="form__label-span required"> Наименование товара </span>
      <input
        v-model.trim="product.name"
        class="form__label-input"
        type="text"
        placeholder="Введите наименование товара"
      />
    </label>
    <label class="form__label">
      <span class="form__label-span"> Описание товара </span>
      <textarea
        v-model.trim="product.description"
        class="form__label-input large"
        type="text"
        placeholder="Введите описание товара"
      />
    </label>
    <label class="form__label">
      <span class="form__label-span required"> Ссылка на изображение товара </span>
      <input
        v-model.trim="product.imageSrc"
        class="form__label-input"
        type="text"
        placeholder="Введите ссылку"
      />
    </label>
    <label class="form__label">
      <span class="form__label-span required"> Цена товара </span>
      <input
        v-model="formatPrice"
        class="form__label-input"
        type="text"
        placeholder="Введите цену"
      />
    </label>
    <button class="form__submit btn-reset" type="submit" :disabled="!isFormFilled"> Добавить товар </button>
    <span v-if="succesAdded" class="form__success">Товар успешно добавлен!</span>
  </form>
</template>

<script>
export default {
  data () {
    return {
      product: {},
      succesAdded: false
    }
  },
  computed: {
    isFormFilled () {
      return this.product.name && this.product.imageSrc && this.product.price
    },
    formatPrice: {
      get () {
        return this.product.price
      },
      set (value) {
        const withoutSpace = value.replace(/\s/g, '')
        this.product.price = new Intl.NumberFormat().format(Number(withoutSpace))
      }
    }
  },
  methods: {
    addProduct () {
      this.succesAdded = false
      this.product.id = Date.now()
      this.product.name = this.product.name.toLowerCase()
      this.product.price = Number(this.product.price.replace(/\s/g, ''))
      this.$emit('addProduct', this.product)
      this.succesAdded = true
      this.product = {}
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';
@import '@/assets/scss/mixins.scss';

.form {
  @include flexColumn;
  position: relative;
  padding: 24px;
  width: 332px;
  background-color: $background;
  box-shadow: $shadowLarge;

  &__label {
    @include flexColumn;
    margin-bottom: 16px;
    width: 100%;

    &-span {
      @include fontOptions(10px, 100%);
      position: relative;
      margin-bottom: 4px;
      align-self: flex-start;

      &.required::after {
        @include size(3px, 3px);
        content: "";
        position: absolute;
        right: -4px;
        top: -1px;
        background-color: $deleteColor;
        border-radius: 100%;
      }
    }

    &-input {
      @include fontOptions(12px, 15px);
      @include transition(border-color);
      padding: 10px 16px;
      height: 36px;
      border: 1px solid transparent;
      border-radius: 4px;
      background-color: $background;
      box-shadow: $shadowSmall;

      &.large {
        height: 108px;
        resize: none;
      }

      &:hover:not(:focus) {
        border-color: $grey;
      }

      &:focus {
        border-color: $textColor;
      }
    }
  }

  &__success {
    @include fontOptions(12px, 15px);
    position: absolute;
    bottom: 5px;
    left: 24px;
    color: $successColor
  }

  &__submit {
    @include fontOptions(12px, 15px);
    @include transition(background-color);
    margin-top: 24px;
    padding: 10px 20px;
    background-color: $successColor;
    border-radius: 10px;
    color: $white;

    &:hover {
      background-color: darken($successColor, 20%);
    }

    &:active {
      background-color: darken($successColor, 30%);
    }

    &:focus-within:not(:active) {
      background-color: darken($successColor, 10%);
    }

    &:disabled {
      background-color: $grey;
      cursor: default;
    }
  }
}

@media (max-width: 499px) {
  .form {
    width: 100%;
  }
}
</style>
