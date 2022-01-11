<template>
  <div>
    <ProductDisplay
      :cart="cart"
      :premium="premium"
      @add-to-cart="addCart"
      @reduce-cart="reduceCart"
    />
  </div>
</template>

<script>
import ProductDisplay from "./components/ProductDisplay";

export default {
  name: "App",
  data() {
    return {
      cart: [],
      premium: true
    };
  },
  components: {
    ProductDisplay
  },
  methods: {
    addCart(id) {
      this.cart.push(id);
    },
    reduceCart(id) {
      this.cart.splice(this.cart.indexOf(id), 1);
    }
  }
};
</script>

