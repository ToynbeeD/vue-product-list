<template>
  <div class="wrapper">
    <select class="select">
      <option value="" selected>По умолчанию</option>
      <option value="1">По возрастанию цены</option>
      <option value="2">По убыванию цены</option>
      <option value="3">По наименованию</option>
    </select>
    <svg>
      <use xlink:href="@/assets/img/icons.svg#arrow-down"></use>
    </svg>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';
@import '@/assets/scss/mixins.scss';

.wrapper {
  position: relative;

  .select {
    @include fontOptions(12px, 100%);
    padding: 10px 16px;
    padding-right: 20px;
    height: 36px;
    color: $grey;
    border-radius: 4px;
    box-shadow: $shadowSmall;
  }

  svg {
    @include size(8px, 6px);
    position: absolute;
    right: 10px;
    top: calc(50% - 3px);
    fill: none;
    stroke: $grey;
    pointer-events: none;
  }
}
</style>
