<template>
  <div>
    <input
      type="checkbox"
      :value="item"
      :checked="isChecked"
      @change="CheckWord(item)"
    />
  </div>
</template>

<script>
export default {
  name: "MyInput",
  props: ["item"],
  data() {
    return {
      isChecked: false,
    };
  },
  methods: {
    CheckWord(item) {
      this.$emit("checkwords", item);
      this.isChecked = !this.isChecked;
    },
  },
};
</script>

<style>
</style>