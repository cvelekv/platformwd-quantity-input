<template>
    <div class="displayFlex marginLeft">
        <label>Select quantity:</label>
        <select class="marginLeft" v-model="selected" @change="onChange($event)">
            <option 
            v-for="option in options" 
            v-bind:key="option.id" 
            :value="option.id" 
            >
            {{option.value}}
            </option>
        </select>
        <form v-if="showText" @submit="updateCustomValue" class="marginLeft">
            <input type="text" style="width:50px" v-model="customValue" name="customValue">
            <input type="submit" value="Update" class="marginLeft">
        </form>
    </div>
</template>

<script>
export default {
  name: "quantityinput",
  props: ["value", "selectMin", "selectMax"],
  data() {
    return {
      options: [],
      selected: this.value,
      showText: false,
      customValue: ""
    };
  },
  methods: {
    fillOptions() {
      for (let i = this.selectMin; i < this.selectMax; i++) {
        this.options.push({
          id: i,
          value: i
        });
        if (i === this.selectMax - 1) {
          this.options.push({
            id: this.selectMax,
            value: `${this.selectMax}+`
          });
        }
      }
    },
    onChange(event) {
      event.target.value == this.selectMax
        ? (this.showText = !this.showText)
        : (this.showText = false);
    },
    updateCustomValue(e) {
      e.preventDefault();
      this.$emit("new-value-selected", this.customValue);
      this.customValue = "";
    }
  },
  created() {
    if (
      this.value &&
      (this.value < this.selectMin ||
        this.value > this.selectMax ||
        this.selectMin > this.selectMax)
    ) {
      alert("Error: Input values are invalid");
      return;
    }
    this.fillOptions();
  }
};
</script>
<style>
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
  position: relative;
  left: 2%;
}
.btn:hover {
  background: #666;
}
.displayFlex {
  display: flex;
}
.marginLeft {
  margin-left: 3px;
}
</style>
