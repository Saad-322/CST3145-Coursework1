<template>
  <main>
    <div v-for="product in products" :key="product.id">
      <h2>{{ product.title }}</h2>
      <figure>
        <img v-bind:src="product.image" />
      </figure>
      <p v-html="product.description"></p>
      <p>Price: {{ product.price }}</p>
      <p>Available stock: {{ product.availableInventory }}</p>
      <button @click="addToCart(product)">Add to cart</button>
    </div>
  </main>
</template>
<script>
export default {
  name: "LessonsList",
  // data from fetch
  prop: ['lessons'],
  data() {
    return {};
  },
  methods: {
    addProduct(product) {
      this.$emit("addProduct", product);
    },
  },
};
</script>

