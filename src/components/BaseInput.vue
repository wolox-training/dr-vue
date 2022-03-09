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
      :class="hasError ? 'error-field' : ''"
    />
    <p class="error-message" v-if="hasError">{{ errorMessage }}</p>
  </div>
</template>

<script lang="ts">
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
    hasError: {
      type: Boolean,
      default: false,
    },
    errorMessage: {
      type: String,
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
  text-align: start;
  position: relative;
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

.error-message {
  font-size: 12px;
  color: red;
  margin: 0;
  position: absolute;
  bottom: -15px;
  left: 0;
}

.error-field {
  border: 2px solid red;
}
</style>
