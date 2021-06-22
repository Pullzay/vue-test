<template>
  <div class="catalog-item">
    <div class="catalog-item-wrapper">
      <img
        :src="require('../assets/images/' + cart_item_data.image)"
        alt="img"
      />
      <p class="catalog-item-title">{{ cart_item_data.name }}</p>
      <p class="catalog-item-price">{{ cart_item_data.price }} Р</p>
      <p class="catalog-item-article">{{ cart_item_data.article }} Р</p>
      <p class="catalog-item-quantity">
        <span @click="decrementItem">-</span> {{ cart_item_data.quantity }}
        <span @click="incrementItem">+</span>
      </p>
      <button class="catalog-item-button" @click="deleteFromCart">
        Delete
      </button>
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
    decrementItem() {
      this.$emit("decrement");
    },
    incrementItem() {
      this.$emit("increment");
    },
  },
};
</script>

<style></style>
