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

<style>
.main-wrapper {
  max-width: 900px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}
</style>
