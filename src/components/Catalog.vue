<template>
  <div class="catalog">
    <h1>Catalog</h1>
    <CatalogItem />
    <Cart />
  </div>
</template>

<script>
import CatalogItem from "./CatalogItem.vue";
import Cart from "./Cart.vue";

export default {
  name: "Catalog",
  components: {
    CatalogItem,
    Cart,
  },
};
</script>

<style></style>
