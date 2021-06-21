<template>
  <div class="cart">
    <p v-if="!cart_data.length">Корзина пустая</p>
    <div v-if="cart_data.length">
      <h1>Cart</h1>
      <CartItem
        v-for="(item, index) in cart_data"
        :key="item.atricle"
        :cart_item_data="item"
        @deleteFromCart="deleteFromCart(index)"
        @increment="increment(index)"
        @decrement="decrement(index)"
      />
      <div class="cart-total">
        <p>Total: {{ cartTotalCost }} Р</p>
      </div>
    </div>
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
  computed: {
    cartTotalCost() {
      let result = [];

      if (this.cart_data.length) {
        for (let item of this.cart_data) {
          result.push(item.price * item.quantity);
        }

        result = result.reduce(function (sum, el) {
          return sum + el;
        });
      }

      return result;
    },
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
    ...mapActions([
      "DELETE_FROM_CART",
      "INCREMENT_CART_ITEM",
      "DECREMENT_CART_ITEM",
    ]),
    increment(index) {
      this.INCREMENT_CART_ITEM(index);
    },
    decrement(index) {
      this.DECREMENT_CART_ITEM(index);
    },
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index);
    },
  },
};
</script>

<style></style>
