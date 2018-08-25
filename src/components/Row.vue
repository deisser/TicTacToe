<template>
    <div class="row">
        <field></field>
        <field></field>
        <field></field>
    </div>
</template>

<script>
import Field from "./Field";

export default {
  name: "Row",
  props: {
    input: String,
    lastId: Number,
    end: Boolean
  },
  components: {
    Field
  }
};
</script>

<style scoped>
</style>

