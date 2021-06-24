<template>
  <div class="select">
    <p @click="arOptionsVisible = !arOptionsVisible">{{ selected }}</p>
    <div v-if="arOptionsVisible" class="options">
      <p
        v-for="option in options"
        :key="option.value"
        @click="selectOption(option)"
      >
        {{ option.name }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Select",
  props: {
    options: {
      type: Array,
      default: () => [],
    },
    selected: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      arOptionsVisible: false,
    };
  },
  methods: {
    selectOption(option) {
      this.$emit("select", option);
      this.arOptionsVisible = false;
    },
    hideSelect() {
      this.arOptionsVisible = false;
    },
  },
  mounted() {
    document.addEventListener("click", this.hideSelect.bind(this), true);
  },
  beforeDestroy() {
    document.removeEventListener("click", this.hideSelect);
  },
};
</script>
