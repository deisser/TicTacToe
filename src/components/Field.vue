<template>
    <div @click="check()" class="field">{{value}}</div>
</template>

<script>
export default {
  name: "Field",
  data: function() {
    return {
      value: null
    };
  },
  methods: {
    check: function() {
      if (this.$parent.end) {
        if (!this.value) {
          this.value = this.$parent.$props.input;
          this.$parent.$emit("field-event", this._uid);
        } else {
          var id = this.$parent.$props.lastId;
          if (this._uid === id) {
            this.value = null;
            this.$parent.$emit("field-event", this._uid);
          }
        }
      }
    }
  }
};
</script>

<style scoped>
.field {
  border: 1px solid black;
  width: 50px;
  height: 50px;
  font-size: 42px;
}
</style>

