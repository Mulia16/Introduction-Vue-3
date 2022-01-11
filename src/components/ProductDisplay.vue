<template>
  <div>
    <div class="nav-bar"></div>
    <div class="cart">Cart({{ cart.length }})</div>
    <div class="product-display">
      <div class="product-container">
        <div class="product-image">
          <img :src="image" alt="product image" :class="{ 'out-of-stock-img': !inStock }" />
        </div>
        <div class="product-info">
          <h1>{{ title }}</h1>

          <p v-if="inStock">In Stock</p>
          <p v-else>Out of Stock</p>

          <p>Shipping: {{ shipping }}</p>

          <p v-show="onSale">{{ this.itemOnSale }}</p>

          <ProductDetails :details="details" />

          <div
            v-for="(variant, index) in variants"
            :key="variant.id"
            @mouseover="updateVariant(index)"
            class="color-circle"
            :style="{ backgroundColor: variant.color }"
          ></div>

          <p>{{ description }}</p>

          <button
            class="button"
            @click="addCart()"
            :disabled="!inStock"
            :class="{ disabledButton: !inStock }"
          >Add to Cart</button>
          <button
            class="button"
            @click="reduceCart()"
            :disabled="canReduce"
            :class="{ disabledButton: canReduce }"
          >Reduce from Cart</button>
        </div>
      </div>
      <a :href="url_github" target="_blank">github</a>
    </div>
    <ReviewList :reviews="reviews" v-show="reviews.length" />
    <ReviewForm @review-submitted="addReview" />
  </div>
</template>

<script>
import ProductDetails from "./ProductDetails";
import ReviewForm from "./ReviewForm";
import ReviewList from "./ReviewList";

export default {
  name: "product-display",
  props: {
    cart: {
      type: Number,
      required: true
    },
    premium: {
      type: Object,
      required: true
    }
  },
  components: {
    ProductDetails,
    ReviewForm,
    ReviewList
  },
  data() {
    return {
      product: "Socks",
      brand: "Vue Mastery",
      description:
        "A garment for the foot and lower part of the leg, typically knitted from wool, cotton, or nylon.",
      selectedVariant: 0,
      url_github: "https://github.com/Code-Pop/Intro-to-Vue-3",
      onSale: true,
      details: ["50% cotton", "30% wool", "20% polyster"],
      variants: [
        {
          id: 2234,
          color: "green",
          image: require("../assets/images/socks_green.jpg"),
          quantity: 50
        },
        {
          id: 2235,
          color: "blue",
          image: require("../assets/images/socks_blue.jpg"),
          quantity: 0
        }
      ],
      reviews: []
    };
  },
  methods: {
    updateVariant(index) {
      this.selectedVariant = index;
    },
    addCart() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].id);
    },
    reduceCart() {
      this.$emit("reduce-cart", this.variants[this.selectedVariant].id);
    },
    addReview(review) {
      this.reviews.push(review);
    }
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].image;
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity;
    },
    itemOnSale() {
      return this.title + " is on sale";
    },
    shipping() {
      return this.premium ? "Free" : 2.99;
    },
    canReduce() {
      return !(this.cart.indexOf(this.variants[this.selectedVariant].id) > -1);
    }
  }
};
</script>

<style>
@import "../assets/styles.css";
</style>