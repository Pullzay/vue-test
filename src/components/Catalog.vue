<template>
  <div class="catalog">
    <router-link
      :to="{ name: 'cart', params: { cart_data: CART } }"
      v-if="CART.length"
    >
      <div class="catalog-cart">Cart {{ CART.length }}</div>
    </router-link>
    <div v-else class="catalog-cart">Cart 0</div>
    <Select
      :options="categories"
      @select="sortByCategoris"
      :selected="selected"
    />
    <CatalogItem
      v-for="product in filteredProducts"
      :key="product.article"
      :product_data="product"
      @addToCart="addToCart"
    />
  </div>
</template>

<script>
import CatalogItem from "./CatalogItem.vue";
import Select from "./Select.vue";
import { mapActions, mapGetters } from "vuex";

export default {
  name: "Catalog",
  components: {
    CatalogItem,
    Select,
  },
  computed: {
    ...mapGetters(["PRODUCTS", "CART"]),
    filteredProducts() {
      if (this.sortedProducts.length) {
        return this.sortedProducts;
      } else {
        return this.PRODUCTS;
      }
    },
  },
  methods: {
    ...mapActions(["GET_PRODUCTS_FROM_API", "ADD_TO_CART"]),
    addToCart(data) {
      this.ADD_TO_CART(data);
    },
    sortByCategoris(category) {
      this.sortedProducts = [];
      let vm = this;
      this.PRODUCTS.map((item) => {
        if (item.category === category.name) {
          vm.sortedProducts.push(item);
        }
      });
      this.selected = category.name;
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
    return {
      categories: [
        { name: "Все", value: "all" },
        { name: "Мужские", value: "man" },
        { name: "Женские", value: "woman" },
      ],
      selected: "Все",
      sortedProducts: [],
    };
  },
};
</script>

<style></style>
