<template>
  <div>
    <form class="review-form" @submit.prevent="onSubmit">
      <h3>Leave a review</h3>
      <label for="name">Name:</label>
      <input type="name" v-model="name" />

      <label for="review">Review:</label>
      <textarea id="review" v-model="review"></textarea>

      <label for="rating">Rating:</label>
      <select id="rating" v-model.number="rating">
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select>

      <br />
      <br />
      <label for="recommend">Would you recommend this product?</label>
      <input
        type="radio"
        name="recommend"
        :value="yes"
        style="all: revert;"
        @click="onChangeRecommend"
        checked
      />
      <label for="yes">Yes</label>
      <input
        type="radio"
        name="recommend"
        :value="no"
        style="all: revert;"
        @click="onChangeRecommend"
      />
      <label for="no">No</label>

      <input class="button" type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
export default {
  name: "review-form",
  data() {
    return {
      name: "",
      review: "",
      rating: null,
      recommend: "yes"
    };
  },
  methods: {
    onSubmit() {
      if (!this.name || !this.review || !this.rating || !this.recommend) {
        alert("Review is incomplete. Please fill out every field.");
      } else {
        let productReview = {
          name: this.name,
          review: this.review,
          rating: this.rating,
          recommend: this.recommend
        };
        console.log(productReview);

        this.$emit("review-submitted", productReview);

        this.name = "";
        this.review = "";
        this.rating = null;
        this.recommend = null;
      }
    },
    onChangeRecommend(event) {
      console.log(event);
      this.recommend = event.target.value;
    }
  }
};
</script>

<style>
@import "../assets/styles.css";
</style>