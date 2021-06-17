<template>
  <div class="cart">
    <h1>Cart</h1>
    <CartItem
      v-for="item in cart_data"
      :key="item.atricle"
      :cart_item_data="item"
    />
  </div>
</template>

<script>
import CartItem from "./CartItem.vue";

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
};
</script>

<style></style>
