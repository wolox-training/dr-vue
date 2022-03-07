<template>
  <button v-bind="$attrs" @click="handleClick">
    {{ label }}
  </button>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: "",
    },
    handleClick: {
      type: Function,
      // eslint-disable-next-line @typescript-eslint/no-empty-function
      default: () => {},
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
