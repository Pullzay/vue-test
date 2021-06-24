<template>
  <div class="main-wrapper">
    <Select :options="options" @select="optionSelect" :selected="selected" />
    <keep-alive>
      <router-view> </router-view>
    </keep-alive>
  </div>
</template>

<script>
import Select from "./Select.vue";

export default {
  components: {
    Select,
  },
  name: "MainWrapper",
  data() {
    return {
      options: [
        { name: "Option 1", value: 1 },
        { name: "Option 2", value: 2 },
        { name: "Option 3", value: 3 },
        { name: "Option 4", value: 4 },
        { name: "Option 5", value: 5 },
      ],
      selected: "Select",
    };
  },
  methods: {
    optionSelect(option) {
      this.selected = option.name;
    },
  },
};
</script>
