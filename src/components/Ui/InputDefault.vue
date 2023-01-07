<template>
  <input :value="modelValue" @input="updateValue" class="input" type="text" />
</template>
<script>
export default {
  name: "input-default",
  props: {
    modelValue: [String, Number],
  },
  methods: {
    updateValue(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>
<style>
.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-bottom: 15px;
}
</style>
