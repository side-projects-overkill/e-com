<script setup>
import "@patternfly/pfe-card";
import "@rhds/elements/rh-spinner/rh-spinner.js";
import { useProductStore } from "../stores/products.js";
import router from "../routes";
const productStore = useProductStore();
const productDetailPage = (modelName, id) => {

  router.push(`/product-details?category=${productStore.categoryName}&product=${modelName}&id=${id}`);

}
console.log(productStore.productLists);
console.log(productStore.categoryName);

console.log(productStore.productLists);

</script>

<template>
  <div class="category-box-cards">
    <div class="pfe-l-bullseye">
      <div>
        <h1 v-if="productStore.isLoading" class="server-message">
          <rh-spinner></rh-spinner>
        </h1>
        <h1 v-if="!productStore.isLoading && (productStore.showError || !productStore.productLists.length)" class="server-message">
          Sorry,No Data Found!!!
        </h1>

      </div>
     
    </div>
   
    <div class="pfe-l-grid pfe-m-gutters pfe-m-all-3-col">
      <pfe-card v-if="!productStore.isLoading && !productStore.showError && productStore.productLists.length
        " class="category-card" v-for="(product, index) in productStore.productLists"
        @click="productDetailPage(product.modelName, product.id)">
        <img :src="product.image" alt="image" class="category-card-image" />
        <div slot="pfe-card--footer">
          <h3>{{ product.modelName }}</h3>
          <h3>&#8377; {{ product.price }}</h3>
        </div>
      </pfe-card>
    </div>
  </div>
</template>

<style scoped>
.category-box-cards {
  margin-top: 2rem;
  width: 100%;
 
 
}

.server-message {
  text-align: center;
  height: 40vh;
  width: 100%;
  margin: auto;
}

.category-card {
  height: 25rem;
  width: 22rem;
  margin: 2rem auto;
  cursor: pointer;
  border-radius: 25px;
}

.category-card-image {
  height: 15rem;
  width: 100%;
}
</style>
