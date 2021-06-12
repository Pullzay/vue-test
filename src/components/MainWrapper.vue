<template>
  <div class="main-wrapper">
    <p>{{ title }}</p>
    <Catalog />
  </div>
</template>

<script>
import Catalog from "./Catalog.vue";

export default {
  name: "MainWrapper",
  components: {
    Catalog,
  },
  props: {},
  data() {
    return {
      title: "Azaza",
    };
  },
  computed: {},
  methods: {},
  watch: {},
};
</script>
