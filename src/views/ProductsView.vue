<template>
  <div class="container">
    <div class="flex justify-center py-5 px-20">
      <h1 class="text-5xl font-bold">Our Products</h1>
    </div>
    <div class="grid md:grid-cols-4 gap-4 px-10 py-5 mx-auto ml-auto">
      <!-- product card -->
      <Products
        class="flex justify-center"
        v-for="(product, index) in inventory"
        :key="product.id"
        :index="index"
        :product="product"
        :addToCart="addToCart"
      />
    </div>
  </div>
</template>

<script>
import Products from "@/components/Products.vue";
export default {
  props: ["inventory", "addToCart"],
  components: {
    Products,
  },
};
</script>

<style>
</style>