<template>
  <div class="container">
    <van-index-bar
        :index-list="indexList"
    >
      <div v-for="(value, key) in categories">
        <van-index-anchor :index="key" />
        <van-cell
            v-for="(product, index) in value"
            :index="index"
            :title="product.title"
        />
      </div>


    </van-index-bar>
  </div>
</template>

<script setup>
// Get fake product data and get list of products
// get unique list of category to be the main indexList for
// the component
import fakeProducts from "~/static/fake-list.json";
const products = fakeProducts.products;
const productCategories = [...new Set(products.map(el => el.category))]

// Helper
function groupBy(arr, property) {
  return arr.reduce(function(memo, x) {
    if (!memo[x[property]]) { memo[x[property]] = []; }
    memo[x[property]].push(x);
    return memo;
  }, {});
}


const indexList = ref(productCategories);
const productList = ref(products)
const categories = ref(groupBy(products, 'category'));


</script>

<style>
.container {
  max-width: 1200px;
  margin: auto;
  min-height: 2000px;
}

/* custom style for the component*/
.van-index-bar__sidebar {
  right: auto;
  top: 0;
  width: 100%;
  background: white;
  flex-direction: row;
  transform: none;
  height: 2rem;
  align-items: center;
  position: sticky;
  border-bottom: 1px solid #ddd;
}

.van-index-bar__index--active {
  background-color: #000;
  color: #fff;
  padding: 0.5rem;
  border-radius: 0.5rem;
}

</style>
