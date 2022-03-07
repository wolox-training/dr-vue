<template>
  <form @submit.prevent="handleOnSubmit">
    <BaseInput v-model="register.first_name" label="Nombre" type="text" />
    <BaseInput v-model="register.last_name" label="Apellido" type="text" />
    <BaseInput v-model="register.email" label="Email" type="email" />
    <BaseInput v-model="register.password" label="Password" type="password" />
    <BaseInput
      v-model="register.password_confirmation"
      label="Confirmacion de Password"
      type="password"
    />
    <BaseButton label="Sing Up" type="submit" />
  </form>
</template>

<script lang="ts">
import { ref, defineComponent } from "vue";
import BaseInput from "@/components/BaseInput.vue";
import BaseButton from "@/components/BaseButton.vue";

export default defineComponent({
  components: {
    BaseInput,
    BaseButton,
  },
  emits: ["onSubmit"],
  setup(_, { emit }) {
    const register = ref({
      first_name: "",
      last_name: "",
      email: "",
      password: "",
      password_confirmation: "",
      locale: "en",
    });

    function handleOnSubmit() {
      emit("onSubmit", { ...register.value });
    }

    return { register, handleOnSubmit };
  },
});
</script>

<style lang=""></style>
