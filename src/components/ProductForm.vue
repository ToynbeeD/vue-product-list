<template>
  <form class="form" action="#">
    <label class="form__label">
      <span class="form__label-span required"> Наименование товара </span>
      <input
        class="form__label-input"
        type="text"
        placeholder="Введите наименование товара"
      />
    </label>
    <label class="form__label">
      <span class="form__label-span"> Описание товара </span>
      <textarea
        class="form__label-input large"
        type="text"
        placeholder="Введите описание товара"
      />
    </label>
    <label class="form__label">
      <span class="form__label-span required"> Ссылка на изображение товара </span>
      <input
        class="form__label-input"
        type="text"
        placeholder="Введите ссылку"
      />
    </label>
    <label class="form__label">
      <span class="form__label-span required"> Цена товара </span>
      <input
        class="form__label-input"
        type="text"
        placeholder="Введите цену"
      />
    </label>
    <button class="form__submit btn-reset" type="submit"> Добавить товар </button>
  </form>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';
@import '@/assets/scss/mixins.scss';

.form {
  @include flexColumn;
  padding: 24px;
  margin-right: 16px;
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
      padding: 10px 16px;
      height: 36px;
      border-radius: 4px;
      background-color: $background;
      box-shadow: $shadowSmall;

      &.large {
        height: 108px;
        resize: none;
      }
    }
  }

  &__submit {
    @include fontOptions(12px, 15px);
    margin-top: 24px;
    padding: 10px 20px;
    background-color: $successColor;
    border-radius: 10px;
    color: $white;
  }
}
</style>
