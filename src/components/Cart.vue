<template>
  <div class="cart">
    <p v-if="!cart_data.length">Корзина пустая</p>
    <h1>Cart</h1>
    <CartItem
      v-for="(item, index) in cart_data"
      :key="item.atricle"
      :cart_item_data="item"
      @deleteFromCart="deleteFromCart(index)"
    />
    <router-link :to="{ name: 'catalog' }">
      <div class="catalog-cart">Home</div>
    </router-link>
  </div>
</template>

<script>
import CartItem from "./CartItem.vue";
import { mapActions } from "vuex";

export default {
  name: "Cart",
  components: {
    CartItem,
  },
  props: {
    cart_data: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  methods: {
    ...mapActions(["DELETE_FROM_CART"]),
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index);
    },
  },
};
</script>

<style></style>
