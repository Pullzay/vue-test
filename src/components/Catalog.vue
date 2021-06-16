<template>
  <div class="catalog">
    <CatalogItem
      v-for="product in PRODUCTS"
      :key="product.article"
      :product_data="product"
      @sendDataToParent="showChildArticle"
    />
    <Cart />
  </div>
</template>

<script>
import CatalogItem from "./CatalogItem.vue";
import Cart from "./Cart.vue";
import { mapActions, mapGetters } from "vuex";

export default {
  name: "Catalog",
  components: {
    CatalogItem,
    Cart,
  },
  computed: {
    ...mapGetters(["PRODUCTS"]),
  },
  methods: {
    ...mapActions(["GET_PRODUCTS_FROM_API"]),
    showChildArticle(data) {
      console.log(data);
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
