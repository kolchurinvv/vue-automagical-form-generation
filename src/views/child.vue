<template>
  <div>
    <label :for="Object.keys(item).toString()"
      >{{ Object.keys(item).toString() }} {{ value }}</label
    >
    <input
      type="text"
      class="my-button"
      :value="value[Object.keys(item).toString()]"
      @input="userInput($event)"
      :id="Object.keys(item).toString()"
      :placeholder="item[Object.keys(item).toString()]"
    />
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "ChildComponent",
  props: {
    item: {
      type: Object
    },
    value: {
      type: Object,
      required: false,
      default() {
        return "";
      }
    }
  },
  methods: {
    userInput(val) {
      this.$emit("user-input", val);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">
.my-button
  display: inline-block
  border: 2px solid black
</style>
