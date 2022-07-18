<template>
  <div class="wrapper">
    <select @change="doSort" class="select" v-model="sortKey">
      <option value="" selected>По умолчанию</option>
      <option value="price-up">По возрастанию цены</option>
      <option value="price-down">По убыванию цены</option>
      <option value="name">По наименованию</option>
    </select>
    <svg>
      <use xlink:href="@/assets/img/icons.svg#arrow-down"></use>
    </svg>
  </div>
</template>

<script>
export default {
  data () {
    return {
      sortKey: ''
    }
  },
  methods: {
    doSort () {
      this.$emit('sort', this.sortKey)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';
@import '@/assets/scss/mixins.scss';

.wrapper {
  position: relative;

  &:hover {
    .select {
      color: $textColor
    }

    svg {
      stroke: $textColor;
    }
  }

  .select {
    @include fontOptions(12px, 100%);
    @include transition(color);
    padding: 10px 16px;
    padding-right: 20px;
    height: 36px;
    color: $grey;
    border-radius: 4px;
    box-shadow: $shadowSmall;

    &:focus {
      color: $textColor
    }

    &:focus ~ svg {
      stroke: $textColor;
    }
  }

  svg {
    @include size(8px, 6px);
    @include transition(stroke);
    position: absolute;
    right: 10px;
    top: calc(50% - 3px);
    fill: none;
    stroke: $grey;
    pointer-events: none;
  }
}
</style>
