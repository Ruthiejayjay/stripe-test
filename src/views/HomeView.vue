<template>
  <div class="home">
    <HeaderCom />
    <div class="container">
      <div class="flex justify-center py-5 px-20">
        <h1 class="text-5xl font-bold">Our Products</h1>
      </div>
      <div class="grid md:grid-cols-4 gap-4 px-10 py-5 mx-auto ml-auto">
        <!-- product card -->
        <Products 
          class="flex justify-center" 
          v-for="(product, index) in inventory.slice(0, 4)" 
          :key="product.id" 
          :index="index"
          :product="product"
          :addToCart="addToCart"
        />
          
        
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import HeaderCom from "@/components/HeaderCom.vue";
import Products from "@/components/Products.vue";
export default {
  name: "HomeView", 
  props: ['inventory', 'addToCart'],
  components: {
    HeaderCom,
    Products,
  },
};
</script>
