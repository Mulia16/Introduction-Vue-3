<template>
  <div class="review-container">
    <h3>Reviews:</h3>
    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        {{ review.name }} gave this {{ review.rating }} stars and he/she {{ review.recommend === "yes" ? "recommended" : "not recommended"}} this product
        <br />
        "{{ review.review }}""
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "review-list",
  props: {
    reviews: {
      type: Array,
      required: true
    }
  }
};
</script>

<style>
@import "../assets/styles.css";
</style>