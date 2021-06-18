<template>
  <div class="catalog">
    <div class="catalog_item">
      <img
        :src="require('../assets/images/' + cart_item_data.image)"
        alt="img"
      />
      <p>{{ cart_item_data.name }}</p>
      <p>{{ cart_item_data.price }} Р</p>
      <p>{{ cart_item_data.article }} Р</p>
      <p>{{ cart_item_data.quantity }}</p>
      <button @click="deleteFromCart">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CartItem",
  props: {
    cart_item_data: {
      type: Object,
      default() {
        return [];
      },
    },
  },
  methods: {
    deleteFromCart() {
      this.$emit("deleteFromCart");
    },
  },
  mounted() {
    this.$set(this.cart_item_data, "quantity", 1);
  },
};
</script>

<style></style>
