<template>
  <div class="notification">
    <transition-group name="transition-animate" class="messages">
      <div
        class="notification-content"
        v-for="message in messages"
        :key="message.id"
      >
        <div class="notification-text">
          <span>{{ message.name }}</span>
          <i class="material-icons">check_circle</i>
        </div>
        <div class="notification-buttons">
          <button v-if="rightButton.length">{{ rightButton }}</button>
          <button v-if="leftButton.length">{{ leftButton }}</button>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "Notification",
  props: {
    messages: {
      type: Array,
      default: () => {
        return [];
      },
    },
    rightButton: {
      type: String,
      default: "",
    },
    leftButton: {
      type: String,
      default: "",
    },
    timeout: {
      type: Number,
      default: 3000,
    },
  },
  methods: {
    hideNotification() {
      if (this.messages.length) {
        setTimeout(() => {
          this.messages.splice(this.messages.length - 1, 1);
        }, this.timeout);
      }
    },
  },
  watch: {
    messages() {
      this.hideNotification();
    },
  },
  mounted() {
    this.hideNotification();
  },
};
</script>
