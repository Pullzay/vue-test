<template>
  <div class="catalog-item">
    <img :src="require('../assets/images/' + product_data.image)" alt="img" />
    <p>{{ product_data.name }}</p>
    <p>{{ product_data.price }} Р</p>
    <button @click="addToCart">Add to cart</button>
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
