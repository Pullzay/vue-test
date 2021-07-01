<template>
  <div class="popup-wrapper" ref="popup_wrapper">
    <div class="popup">
      <div class="popup-header">
        <span>{{ popupTitle }}</span>
        <span><i @click="closePopup" class="material-icons">close</i></span>
      </div>
      <div class="popup-content">
        <slot></slot>
      </div>
      <div class="popup-footer">
        <button class="close-modal" @click="closePopup">Close</button>
        <button class="btn" @click="rightButtonAction">
          {{ rightButtonTitle }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Popup",
  methods: {
    closePopup() {
      this.$emit("closePopup");
    },
    rightButtonAction() {
      this.$emit("rightButtonAction");
    },
  },
  mounted() {
    document.addEventListener("click", (item) => {
      if (item.target === this.$refs["popup_wrapper"]) {
        this.closePopup();
      }
    });
  },
  props: {
    rightButtonTitle: {
      type: String,
      default: "Ok",
    },
    popupTitle: {
      type: String,
      default: "Popup name",
    },
  },
};
</script>
