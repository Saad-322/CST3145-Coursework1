<template>
  <div id="app">
    <div v-if="showProduct">
      <button @click="showCheckout">{{ this.cart.length }} Checkout</button>
      <lessons :lessonList="lessonList" @addToCart="addToCart"></lessons>
    </div>
    <div v-else>
      <checkout
        :cart="cart"
        @showCheckout="showCheckout"
        @removeFromCart="removeFromCart"
      ></checkout>
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
      cart: [],
      lessonList: [],
      showProduct: "false",
    };
  },
  components: { lessons, checkout },
  methods: {
    showCheckout() {
      return (this.showProduct = this.showProduct ? false : true);
    },
    addToCart(lesson) {
      this.cart.push(lesson);
      lesson.Spaces--;
    },
    removeFromCart(lesson) {
      let index = this.cart.indexOf(lesson);
      this.cart.splice(index, 1);
      lesson.Spaces++
    },
    displayData() {
      let self = this;
      fetch("https://cst-3145-cw2.herokuapp.com/collection/lessons").then(
        function (response) {
          response.json().then(function (json) {
            self.lessonList = json;
          });
        }
      );
    },
  },
  mounted() {
    this.displayData();
  },
};
</script>