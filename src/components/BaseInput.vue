<template>
  <div class="field-container">
    <label v-if="label" class="label">{{ label }}</label>
    <input
      v-bind="$attrs"
      :value="modelValue"
      :placeholder="label"
      autocomplete="off"
      @input="$emit('update:modelValue', $event.target.value)"
      class="field"
    />
  </div>
</template>

<script>
export default {
  emits: ["update:modelValue"],
  props: {
    label: {
      type: String,
      default: "",
    },
    modelValue: {
      type: [String, Number],
      default: "",
    },
  },
};
</script>

<style lang="scss" scoped>
.field-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

.label {
  align-self: flex-start;
  font-weight: bold;
}

.field {
  height: 35px;
  padding: 0 5px;
  border: none;
  border-radius: 5px;
}
</style>
