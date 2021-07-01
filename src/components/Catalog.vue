<template>
  <div class="catalog">
    <router-link
      :to="{ name: 'cart', params: { cart_data: CART } }"
      v-if="CART.length"
    >
      <div class="catalog-cart">Cart {{ CART.length }}</div>
    </router-link>
    <div v-else class="catalog-cart">Cart 0</div>
    <div class="filters">
      <Select
        :options="categories"
        @select="sortByCategories"
        :selected="selected"
      />
      <div class="range-slider">
        <input
          type="range"
          min="0"
          max="9000"
          step="10"
          v-model.number="minPrice"
          @change="setRangeSlider"
        />
        <input
          type="range"
          min="0"
          max="9000"
          step="10"
          v-model.number="maxPrice"
          @change="setRangeSlider"
        />
      </div>
      <div class="range-values">
        <p>Min: {{ minPrice }}</p>
        <p>Max: {{ maxPrice }}</p>
      </div>
    </div>
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
    sortByCategories(category) {
      this.sortedProducts = [...this.PRODUCTS];
      this.sortedProducts = this.sortedProducts.filter((item) => {
        return item.price >= this.minPrice && item.price <= this.maxPrice;
      });
      if (category) {
        this.sortedProducts = this.sortedProducts.filter((e) => {
          this.selected = category.name;
          return e.category === category.name;
        });
      }
    },
    setRangeSlider() {
      if (this.minPrice > this.maxPrice) {
        let tmp = this.maxPrice;
        this.maxPrice = this.minPrice;
        this.minPrice = tmp;
      }
      this.sortByCategories();
    },
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API().then((responce) => {
      if (responce.data) {
        this.sortByCategories();
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
      minPrice: 0,
      maxPrice: 9000,
    };
  },
};
</script>
