<template>
  <div>
    <div>data: info = {{ info }}</div>
    <hr />
    <child
      v-for="item in info"
      :key="Object.keys(item).toString()"
      @user-input="update"
      v-model="values"
      :item="item"
    >
      <ul v-if="selectionsVisible[Object.keys(item).toString()]">
        <li
          @click="clicked($event)"
          v-for="line in selections[Object.keys(item).toString()]"
          :key="line.index"
          :for="Object.keys(item).toString()"
        >
          {{ line }} for input of "{{ values[Object.keys(item).toString()] }}"
        </li>
      </ul>
      <hr />
    </child>
  </div>
</template>

<script>
import Child from "@/views/child.vue";
export default {
  name: "HelloWorld",
  components: {
    Child
  },
  methods: {
    update(info) {
      if (!info.target.value) {
        setTimeout(() => {
          this.selectionsVisible[info.target.id] = false;
        }, 1000);
      }
      let input = { [info.target.id]: info.target.value };
      this.values = { ...this.values, ...input };
      this.selectionsVisible[info.target.id] = true;
      this.$emit("updated");
    },
    clicked(val) {
      let selection = {
        [val.target.attributes.getNamedItem("for").value]:
          val.target.textContent.trim() + " was clicked"
      };
      this.selectionsVisible[
        val.target.attributes.getNamedItem("for").value
      ] = false;
      this.values = { ...this.values, ...selection };
      this.$emit("clicked", this.values);
    }
  },
  data() {
    return {
      info: [{ firstID: "orginal info #1" }, { secondID: "original info #2" }],
      selectionsVisible: { firstID: false, secondID: false },
      values: {},
      selections: {
        firstID: ["firstID #1 option", "firstID #2 option"],
        secondID: ["secondID #1 option", "secondID #2 option"]
      }
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
