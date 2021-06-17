<template>
  <div class="main-wrapper">
    <Catalog />
    <Cart v-if="CART.length" :cart_data="CART" />
  </div>
</template>

<script>
import Catalog from "./Catalog.vue";
import Cart from "./Cart.vue";
import { mapGetters } from "vuex";

export default {
  name: "MainWrapper",
  components: {
    Catalog,
    Cart,
  },
  computed: {
    ...mapGetters(["CART"]),
  },
};
</script>
