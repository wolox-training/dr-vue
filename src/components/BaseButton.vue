<template>
  <button v-bind="$attrs" @click="handleClick" class="button" :class="variant">
    {{ label }}
  </button>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

export default defineComponent({
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
    variant: {
      type: String as PropType<"primary" | "secondary">,
      default: "primary",
    },
  },
});
</script>

<style lang="scss" scoped>
.button {
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;

  &.primary {
    background-color: #bed23c;
    color: white;
    border: none;
  }

  &.secondary {
    border: 2px solid #bed23c;
    color: #bed23c;
    background-color: transparent;
  }

  &:disabled {
    opacity: 0.5;
    cursor: none;
  }
}

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
