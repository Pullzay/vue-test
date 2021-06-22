<template>
  <div class="catalog-item">
    <div class="catalog-item-wrapper">
      <img :src="require('../assets/images/' + product_data.image)" alt="img" />
      <p class="catalog-item-title">{{ product_data.name }}</p>
      <p class="catalog-item-price">{{ product_data.price }} Р</p>
      <button class="catalog-item-button" @click="addToCart">
        Add to cart
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CatalogItem",
  props: {
    product_data: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  methods: {
    addToCart() {
      this.$emit("addToCart", this.product_data);
    },
  },
  mounted() {
    this.$set(this.product_data, "quantity", 1);
  },
};
</script>

<style></style>
