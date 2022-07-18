<template>
  <div id="app">
    <header class="header">
      <div class="header__container container">
        <h1 class="header__heading">Добавление товара</h1>
        <SortSelect @sort="doSortList" class="header__sort" />
      </div>
    </header>
    <main class="main">
      <div class="main__container container">
        <aside>
          <ProductForm @addProduct="addProductToList" />
        </aside>
        <ProductList @deleteProduct="deleteProduct" :products-list="productsList" />
      </div>
    </main>
  </div>
</template>

<script>
import ProductList from '@/components/ProductList.vue'
import ProductForm from '@/components/ProductForm.vue'
import SortSelect from '@/components/SortSelect.vue'

export default {
  components: { ProductList, ProductForm, SortSelect },
  data () {
    return {
      productsList: []
    }
  },
  methods: {
    createProductList () {
      if (localStorage.products) {
        this.productsList = JSON.parse(localStorage.products)
      } else {
        for (let i = 0; i < 12; i++) {
          const product = {
            id: Date.now() + i,
            name: 'название товара',
            price: 10000,
            imageSrc: require('@/assets/img/product.jpg'),
            description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк'
          }
          this.productsList.push(product)
        }
      }
    },
    addProductToList (product) {
      this.productsList = [product, ...this.productsList]
      localStorage.setItem('products', JSON.stringify(this.productsList))
    },
    deleteProduct (product) {
      this.productsList = this.productsList.filter(item => item.id !== product.id)
      localStorage.setItem('products', JSON.stringify(this.productsList))
    },
    sortingList (key, direction = true) {
      this.productsList = this.productsList.sort((curr, next) => {
        if (curr[key] > next[key]) {
          return direction ? 1 : -1
        }
        if (curr[key] < next[key]) {
          return direction ? -1 : 1
        }
        return 0
      })
    },
    doSortList (sortKey) {
      switch (sortKey) {
        case 'price-up':
          this.sortingList('price')
          break

        case 'price-down':
          this.sortingList('price', false)
          break

        case 'name':
          this.sortingList('name')
          break

        default:
          this.sortingList('id', false)
      }
    }
  },
  created () {
    this.createProductList()
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;600&display=swap');
@import '@/assets/scss/variables.scss';
@import '@/assets/scss/mixins.scss';

* {
  margin: 0;
  padding: 0;
  border: none;
  outline: none;
  box-sizing: border-box;
  font-family: $fontFamily, sans-serif;
}

html,
body {
  margin: 0 auto;
  max-width: 1920px;
}

ul {
  list-style: none;
}

path {
  fill: inherit;
  stroke: inherit;
}

button {
  background-color: transparent;
  cursor: pointer;
}

input,
select,
textarea {
  -webkit-appearance: none;
}

#app {
  background-color: $backgroundLight;
}

.container {
  margin: 0 auto;
  padding: 0 32px;
  max-width: $container;
}

.header {
  padding: 16px 0;

  &__container {
    @include flex(center)
  }

  &__heading {
    @include fontOptions(28px, 100%);
    color: $textColor;
  }

  &__sort {
    margin-left: auto;
  }
}

.main {
  &__container {
    @include flex(flex-start);
  }
}
</style>
