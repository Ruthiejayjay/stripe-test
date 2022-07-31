<template>
  <div
    class="bg-blue-900 text-white sm:flex sm:justify-between sm:px-4 sm:py-3 app"
  >
    <div class="flex items-center justify-between px-4 py-2 sm:0">
      <div class="sm:hidden">
        <button
          @click="isOpen = !isOpen"
          type="button"
          class="focus:text-white focus:outline-none"
        >
          <img v-if="isOpen" src="@/assets/close.png" alt="" class="h-5 w-5" />
          <img v-if="!isOpen" src="@/assets/menu.svg" alt="" class="h-5 w-5" />
        </button>
      </div>
    </div>
    <div :class="isOpen ? 'block' : 'hidden'" class="mb-3 px-2 pt-2 sm:flex">
      <router-link
        to="/"
        class="block px-2 font-semibold rounded hover:bg-blue-500"
        >Home</router-link
      >
      <router-link
        to="/products"
        class="block px-2 font-semibold rounded hover:bg-blue-500"
        >Products</router-link
      >
      <button
        @click="toggleSidebar"
        class="block px-2 font-semibold rounded hover:bg-blue-500"
      >
        Cart ({{ totalQuantity }})
      </button>
    </div>
  </div>
  <router-view :inventory="inventory" :addToCart="addToCart"/>
  <Sidebar 
    v-if="showSidebar" 
    :toggle="toggleSidebar" 
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"

    />
  <Foot />
</template>

<script>
import "./assets/tailwind.css";
import products from "@/Product.json";
import Sidebar from "@/components/Sidebar.vue";
import Foot from "@/components/Foot.vue";
export default {
  data() {
    return {
      isOpen: false,
      showSidebar:false,
      inventory: products,
      cart: {},
    }
  },
  components: {
    Sidebar,
    Foot,
  },
  methods: {
    toggleSidebar() {
      this.showSidebar= !this.showSidebar
    },
    addToCart(name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0;
      this.cart[name] += quantity
    },
    removeItem(name) {
      delete this.cart[name]
    }
  },
  computed: {
    totalQuantity() {
      return Object.values(this.cart).reduce((acc, curr, index) => {
        return acc + curr;
      }, 0);
    },
  },
};
</script>
<style scoped>
.app{ 
  position: relative;
}
</style>
