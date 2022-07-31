<template>
  <nav class="flex flex-col w-96 h-screen px-4 py-8 bg-white border-r sidebar">
    <div class="">
      <div class="flex justify-between">
        <h2 class="font-bold text-blue-600 text-lg sm:text-3xl">Cart</h2>
        <button
          @click="toggle"
          type="button"
          class="
            inline-block
            px-6
            py-2.5
            bg-red-600
            text-white
            font-medium
            text-xs
            leading-tight
            uppercase
            rounded
            shadow-md
            hover:bg-red-700 hover:shadow-lg
            focus:bg-red-700 focus:shadow-lg focus:outline-none focus:ring-0
            active:bg-red-800 active:shadow-lg
            transition
            duration-150
            ease-in-out
          "
        >
          Close
        </button>
      </div>
      <!-- <i class="fa-solid fa-cart-shopping"></i> -->
      <div class="my-10 border border-gray-800"></div>
      <div class="flex flex-col items-left lg:flex-row">
        <div class="flex flex-col">
          <div class="w-full">
            <div class="border-b border-gray-200 shadow">
              <table class="divide-y divide-gray-300">
                <thead class="bg-gray-50">
                  <tr>
                    <th class="px-3 py-2 text-xs text-gray-500">Product</th>
                    <th class="px-3 py-2 text-xs text-gray-500">Qty</th>
                    <th class="px-3 py-2 text-xs text-gray-500">Price</th>
                    <th class="px-3 py-2 text-xs text-gray-500">Total</th>
                    <th class="px-3 py-2 text-xs text-gray-500">Delete</th>
                  </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-300">
                  <tr
                    v-for="(quantity, key, i) in cart"
                    :key="i"
                    class="whitespace-nowrap"
                  >
                    <td class="px-3 py-2 text-sm text-gray-500">{{ key }}</td>
                    <td class="px-3 py-2">
                      <div class="text-sm text-gray-900">{{ quantity }}</div>
                    </td>
                    <td class="px-3 py-2">
                      <div class="text-sm text-gray-500">
                        &#8358; {{ getPrice(key) }}
                      </div>
                    </td>
                    <td class="px-3 py-2 text-sm text-gray-500">
                      &#8358; {{ quantity * getPrice(key) }}
                    </td>
                    <td class="px-3 py-2">
                      <div @click="remove(key)">
                        <svg
                          xmlns="http://www.w3.org/2000/svg"
                          class="w-6 h-6 text-red-400"
                          fill="none"
                          viewBox="0 0 24 24"
                          stroke="currentColor"
                        >
                          <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
                          />
                        </svg>
                      </div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
      <p class="text-center text-lg py-5" v-if="!Object.keys(cart).length">
        No item in Cart
      </p>
      <div
        class="
          flex flex-col
          items-center
          justify-between
          py-5
          px-10
          mx-auto
          max-w-7xl
          xl:px-12
          lg:flex-row
        "
      >
        <div class="relative mb-6 lg:mb-0">
          <h2
            class="
              w-full
              mx-auto
              mb-2
              text-lg
              font-bold
              leading-none
              text-center text-black
              md:text-lg
              xl:text-lg
              lg:text-left
            "
          >
            Total: &#8358; {{ calculateTotal() }}
          </h2>
        </div>
        <button
        @click="checkOut"
          class="
            relative
            flex-shrink-0
            px-4
            py-1
            text-sm
            font-medium
            text-center text-white
            bg-blue-600
            rounded-lg
            lg:text-sm
            focus:ring-4
            focus:ring-blue-600
            focus:ring-opacity-50
            focus:outline-none
          "
        >
          Check Outm
        </button>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from 'axios'
import qs from 'qs'
export default {
  props: ["toggle", "cart", "inventory", "remove"],
  methods: {
    getPrice(name) {
      const product = this.inventory.find((p) => {
        return p.name === name;
      });
      return product.price.NGN;
    },
    getPriceId(name) {
      const product = this.inventory.find((p) => {
        return p.name === name;
      });
      return product.priceId;
    },
    calculateTotal() {
      const total = Object.entries(this.cart).reduce((acc, curr, index) => {
        return acc + curr[1] * this.getPrice(curr[0]);
      }, 0);
      return total.toFixed(2);
    },
    checkOut() {
      console.log('hello');
      var data = qs.stringify({
        mode: "subscription",
        "line_items[0][price]": this.getPriceId,
        "line_items[0][quantity]": quantity,
        cancel_url: "https://example.com/cancel",
        success_url: "https://example.com/success",
      });
      var config = {
        method: "post",
        url: "https://api.stripe.com/v1/checkout/sessions",
        headers: {
          "Content-Type": "application/x-www-form-urlencoded",
          Authorization:
            "Bearer  sk_test_51LIEnMDw37K7KqJsgA0MLKcjUNYnca6j2Fn4VseXUsSaQstpdWUloKZN75KT0Ia4aD48D1h9nMfxyUg36xtbQynz00LyjMYwbk",
        },
        data: data,
      };

      axios(config)
        .then(function (response) {
          console.log(JSON.stringify(response.data));
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
.sidebar {
  position: absolute;
  top: 0;
  right: 0;
}
</style>