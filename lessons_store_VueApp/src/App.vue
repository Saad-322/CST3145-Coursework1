<template>
  <div id="app">
    <div v-if="showProduct">
        <h1>{{ sitename }}</h1>
        <button @click="showCheckout">{{ this.cart.length }} Checkout</button>
        <lessons @addProduct="addToCart"></lessons>
    </div>
    <div v-else>
      <checkout @showCheckout="showCheckout"></checkout>
    </div>
  </div>
</template>
<script>
import lessons from "./components/LessonsList.vue";
import checkout from "./components/Checkout.vue";
export default {
  name: "App",
  data() {
    return {
      sitename: "Vue.js Pet Depot",
      cart: [],
      showProduct: "false",
    };
  },
  components: { lessons,checkout },
  methods: {
    showCheckout() {
      // this.displayData();
      return (this.showProduct = this.showProduct ? false : true);
    },
    addToCart(product) {
      this.cart.push(product);
    },
  },
};
</script>