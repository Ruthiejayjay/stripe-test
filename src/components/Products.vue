<template>
  <div class="flex justify-center">
    <div class="rounded-lg shadow-xl bg-gray-100 max-w-sm">
      <a href="#!">
        <img class="rounded-t-lg" :src="product.image" alt="" />
      </a>
      <div class="p-6">
        <h5 class="text-gray-900 text-xl font-medium mb-2">
          {{ product.name }}
        </h5>
        <h4 class="text-gray-700 text-base mb-2">
          Price: &#8358; {{ product.price.NGN }}
        </h4>
        <div class="mb-2">
          <label for="">Quantity: </label>
          <input type="number" class="mb-1" v-model="quantity" />
        </div>
        <button
          @click="addToCart(product.name, quantity)"
          type="button"
          class="
            inline-block
            px-6
            py-2.5
            bg-blue-600
            text-white
            font-medium
            text-xs
            leading-tight
            uppercase
            rounded
            shadow-md
            hover:bg-blue-700 hover:shadow-lg
            focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0
            active:bg-blue-800 active:shadow-lg
            transition
            duration-150
            ease-in-out
          "
        >
          Add to Cart
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    props: ['product','index', 'addToCart'],
    data() {
        return {
            quantity: 0
        }
    }
};
</script>

<style>
</style>