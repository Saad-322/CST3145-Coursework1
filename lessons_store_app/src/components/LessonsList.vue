<template>
  <main>
    <div>
      <strong>Search Bar </strong>
      <input type="text" v-model.trim="search" />
      <p>You searched for '{{ search }}'</p>
    </div>
    <ul>
      <div
        v-for="lesson in lessonList"
        :key="lesson.lessonID"
        class="lessonlist"
      >
        <div>
          <img v-bind:src="lesson.Image" alt="" width="100px" height="100px" />
          <br />
          Lesson ID: {{ lesson.lessonID }} <br />
          Subject: {{ lesson.Subject }} <br />
          Location: {{ lesson.Location }} <br />
          Price: £{{ lesson.Price }} <br />
          Available Spaces: {{ lesson.Spaces }} <br />
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
          <button @click="addToCart(lesson)" :disabled="!canAddToCart(lesson)">
            Add to cart
          </button>
        </div>
      </div>
    </ul>
  </main>
</template>
<script>
export default {
  name: "LessonsList",
  props: ["lessonList"],
  data() {
    return {
      search: "",
    };
  },
  methods: {
    showCheckout() {
      this.$emit("showCheckout");
    },
    addToCart(lesson) {
      this.$emit("addToCart", lesson);
    },
    canAddToCart(lesson) {
      return lesson.Spaces > 0;
    },
  },
  computed: {
    
  },
};
</script>

