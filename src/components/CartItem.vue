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
      <p></p>
      <button>Delete</button>
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
};
</script>

<style></style>
