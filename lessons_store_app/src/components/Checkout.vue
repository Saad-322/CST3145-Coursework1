<template>
  <main>
    <button @click="showCheckout()">
      <span > Lessons</span>
    </button>
    <h2>Your cart</h2>
    <div>
      <ul>
        <div v-for="lesson in cart" :key="lesson.lessonID" class="lessonlist">
          <img v-bind:src="lesson.Image" alt="" width="100px" height="100px" />
          <br />
          Lesson ID: {{ lesson.lessonID }} <br />
          Subject: {{ lesson.Subject }} <br />
          Location: {{ lesson.Location }} <br />
          Price: £{{ lesson.Price }} <br />
          <span
            v-for="n in lesson.Rating"
            :key="n.lessonID"
            class="fas fa-star"
          ></span>
          <span
            v-for="n in 5 - lesson.Rating"
            :key="n.lessonID"
            class="far fa-star"
          ></span>
          <br /><br />
          <button @click="removeFromCart(lesson)">Remove from cart</button>
          <br />
        </div>
      </ul>
    </div>
    <div>
      <h2>Details</h2>
      <p>
        <strong>First Name: </strong>
        <input type="text" v-model.trim="order.firstName" />
      </p>
      <p>
        <strong>Last Name: </strong>
        <input type="text" v-model.trim="order.lastName" />
      </p>
      <p>
        <strong>Phone Number: </strong>
        <input type="text" v-model.trim="order.phoneNumber" />
      </p>
      <p>
        <strong>Lesson ID: </strong>
        <input type="text" v-model.trim="order.lessonID" />
      </p>
      <p>
        <strong>Number of Spaces: </strong>
        <input type="number" v-model.trim="order.spaces" />
      </p>
      <input type="checkbox" value="gift" v-model="order.gift" />
      <label>Ship as Gift?</label>
      <br />
      <br />
      <h3>Order Information</h3>
      <p>First Name: {{ order.firstName }}</p>
      <p>Last Name: {{ order.lastName }}</p>
      <p>Phone Number: {{ order.phoneNumber }}</p>
      <p>Lesson ID: {{ order.lessonID }}</p>
      <p>Spaces: {{ order.spaces }}</p>
      <p>Gift: {{ order.gift }}</p>
      <button @click="submitForm()" :disabled="!correctOrderDetails">
        Checkout
      </button>
    </div>
  </main>
</template>
<script>
export default {
  name: "CheckoutForm",
  props: ["cart"],
  data() {
    return {
      showProduct: "false",
      order: {
        firstName: "",
        lastName: "",
        phoneNumber: "",
        lessonID: "",
        spaces: 0,
        gift: false,
      },
    };
  },
  methods: {
    showCheckout() {
      this.$emit("showCheckout");
    },
    submitForm() {
      alert("order successfully submitted");
    },
    removeFromCart(lesson) {
      this.$emit("removeFromCart", lesson);
    },
  },
  computed: {
    correctOrderDetails() {
      let letters = /^[a-z]+$/i;
      let numbers = /^[0-9]+$/i;
      if (
        letters.test(this.order.firstName) &&
        letters.test(this.order.lastName) &&
        numbers.test(this.order.phoneNumber)
      ) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

