<template>
  <main>
    <div>
      <h1>{{ sitename }}</h1>
      <strong>Search Bar</strong>
      <input type="text" v-model.trim="search" />
      <p>You searched for '{{ search }}'</p>
    </div>
    <h3>Sort by</h3>
    <input
      type="radio"
      value="Subject"
      name="attributes"
      v-model="sort.attribute"
    />
    <label>Subject</label><br />
    <input
      type="radio"
      value="Location"
      name="attributes"
      v-model="sort.attribute"
    />
    <label>Location</label><br />
    <input
      type="radio"
      value="Price"
      name="attributes"
      v-model="sort.attribute"
    />
    <label>Price</label><br />
    <input
      type="radio"
      value="Availability"
      name="attributes"
      v-model="sort.attribute"
    />
    <label>Availability</label><br />
    <input
      type="radio"
      value="Rating"
      name="attributes"
      v-model="sort.attribute"
    />
    <label>Rating</label><br /><br />

    <input
      type="radio"
      value="ascending"
      name="order"
      v-model="sort.sortingOrder"
    />
    <label>Ascending</label><br />
    <input
      type="radio"
      value="descending"
      name="order"
      v-model="sort.sortingOrder"
    />
    <label>Descending</label>
    <ul>
      <div v-for="lesson in lessonList" :key="lesson.lessonID" class="lessonlist">
        <div>
          <img v-bind:src="lesson.Image" alt="" width="100px" height="100px" />
          <br />
          Lesson ID: {{ lesson.lessonID }} <br />
          Subject: {{ lesson.Subject }} <br />
          Location: {{ lesson.Location }} <br />
          Price: £{{ lesson.Price }} <br />
          Available Spaces: {{ lesson.Spaces }} <br />
          <!-- <span v-for="n in lesson.Rating" class="fas fa-star"></span>
                        <span v-for="n in 5-lesson.Rating" class="far fa-star"></span> <br><br> -->
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
  props:['lessonList'],
  // data from fetch
  data() {
    return {
      sitename: "Lessons Store",
      search: "",
      sort: {
        attribute: "",
        sortingOrder: "",
      },
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
    //   postSearchValue() {
    //               switch (this.sort.attribute) {
    //                   case "Subject":
    //                       if (this.sort.sortingOrder == "ascending") {
    //                           function compare(a, b) {
    //                               if (a.Subject < b.Subject)
    //                                   return -1;
    //                               if (a.Subject > b.Subject)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       else if (this.sort.sortingOrder == "descending") {
    //                           function compare(a, b) {
    //                               if (a.Subject > b.Subject)
    //                                   return -1;
    //                               if (a.Subject < b.Subject)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       break;
    //                   case "Price":
    //                       if (this.sort.sortingOrder == "ascending") {
    //                           function compare(a, b) {
    //                               if (a.Price < b.Price)
    //                                   return -1;
    //                               if (a.Price > b.Price)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       else if (this.sort.sortingOrder == "descending") {
    //                           function compare(a, b) {
    //                               if (a.Price > b.Price)
    //                                   return -1;
    //                               if (a.Price < b.Price)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       break;
    //                   case "Availability":
    //                       if (this.sort.sortingOrder == "ascending") {
    //                           function compare(a, b) {
    //                               if (a.Spaces < b.Spaces)
    //                                   return -1;
    //                               if (a.Spaces > b.Spaces)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       else if (this.sort.sortingOrder == "descending") {
    //                           function compare(a, b) {
    //                               if (a.Spaces > b.Spaces)
    //                                   return -1;
    //                               if (a.Spaces < b.Spaces)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       break;
    //                   case "Location":
    //                       if (this.sort.sortingOrder == "ascending") {
    //                           function compare(a, b) {
    //                               if (a.Location < b.Location)
    //                                   return -1;
    //                               if (a.Location > b.Location)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       else if (this.sort.sortingOrder == "descending") {
    //                           function compare(a, b) {
    //                               if (a.Location > b.Location)
    //                                   return -1;
    //                               if (a.Location < b.Location)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       break;
    //                   case "Rating":
    //                       if (this.sort.sortingOrder == "ascending") {
    //                           function compare(a, b) {
    //                               if (a.Rating < b.Rating)
    //                                   return -1;
    //                               if (a.Rating > b.Rating)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       else if (this.sort.sortingOrder == "descending") {
    //                           function compare(a, b) {
    //                               if (a.Rating > b.Rating)
    //                                   return -1;
    //                               if (a.Rating < b.Rating)
    //                                   return 1;
    //                               return 0;
    //                           }
    //                       }
    //                       break;
    //               }
    //               if (this.search === "") {
    //                   this.displayData()
    //               }
    //               else {
    //                   fetch('https://cst-3145-cw2.herokuapp.com/search/' + this.search + '/lessons').then(
    //                       function (response) {
    //                           response.json().then(
    //                               function (json) {
    //                                   app.lessons = json
    //                               }
    //                           )
    //                       }
    //                   )
    //               }
    //               return this.lessons.sort(compare)
    //           },
  },
};
</script>

