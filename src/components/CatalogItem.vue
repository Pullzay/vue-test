<template>
  <div class="catalog-item">
    <div class="catalog-item-wrapper">
      <Popup
        v-if="isPopupVisible"
        @closePopup="closePopup"
        @rightButtonAction="addToCart"
        rightButtonTitle="Add to cart"
        :popupTitle="product_data.name"
      >
        <img
          :src="require('../assets/images/' + product_data.image)"
          alt="img"
        />
        <p>{{ product_data.category }}</p>
        <p class="catalog-item-price">{{ product_data.price }} Р</p>
      </Popup>
      <img :src="require('../assets/images/' + product_data.image)" alt="img" />
      <p class="catalog-item-title">{{ product_data.name }}</p>
      <p class="catalog-item-price">{{ product_data.price }} Р</p>
      <button class="show-info" @click="showPopupInfo">Show info</button>
      <button class="catalog-item-button btn" @click="addToCart">
        Add to cart
      </button>
    </div>
  </div>
</template>

<script>
import Popup from "./popup/Popup.vue";

export default {
  name: "CatalogItem",
  components: {
    Popup,
  },
  data() {
    return {
      isPopupVisible: false,
    };
  },
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
    showPopupInfo() {
      this.isPopupVisible = true;
    },
    closePopup() {
      this.isPopupVisible = false;
    },
  },
  mounted() {
    this.$set(this.product_data, "quantity", 1);
  },
};
</script>

<style></style>
