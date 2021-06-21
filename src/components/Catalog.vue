<template>
  <div class="catalog">
    <router-link :to="{ name: 'cart', params: { cart_data: CART } }">
      <div class="catalog-cart">Cart {{ CART.length }}</div>
    </router-link>
    <CatalogItem
      v-for="product in PRODUCTS"
      :key="product.article"
      :product_data="product"
      @addToCart="addToCart"
    />
  </div>
</template>

<script>
import CatalogItem from "./CatalogItem.vue";
import { mapActions, mapGetters } from "vuex";

export default {
  name: "Catalog",
  components: {
    CatalogItem,
  },
  computed: {
    ...mapGetters(["PRODUCTS", "CART"]),
  },
  methods: {
    ...mapActions(["GET_PRODUCTS_FROM_API", "ADD_TO_CART"]),
    addToCart(data) {
      this.ADD_TO_CART(data);
    },
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API().then((responce) => {
      if (responce.data) {
        console.log("Готово");
      }
    });
  },
  data() {
    return {};
  },
};
</script>

<style></style>
