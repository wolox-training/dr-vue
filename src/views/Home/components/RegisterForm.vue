<template>
  <form @submit.prevent="handleOnSubmit" class="form-container">
    <BaseInput
      v-model="register.first_name"
      label="Nombre"
      type="text"
      @blur="handleTouch('first_name')"
      :hasError="!!errorsFields.first_name"
      :errorMessage="errorsFields.first_name"
    />
    <BaseInput
      v-model="register.last_name"
      label="Apellido"
      type="text"
      @blur="handleTouch('last_name')"
      :hasError="!!errorsFields.last_name"
      :errorMessage="errorsFields.last_name"
    />
    <BaseInput
      v-model="register.email"
      label="Email"
      type="email"
      :hasError="!!errorsFields.email"
      :errorMessage="errorsFields.email"
      @blur="handleTouch('email')"
    />
    <BaseInput
      v-model="register.password"
      label="Password"
      type="password"
      @blur="handleTouch('password')"
      :hasError="!!errorsFields.password"
      :errorMessage="errorsFields.password"
    />
    <BaseInput
      v-model="register.password_confirmation"
      label="Confirmacion de Password"
      type="password"
      @blur="handleTouch('password_confirmation')"
      :hasError="!!errorsFields.password_confirmation"
      :errorMessage="errorsFields.password_confirmation"
    />
    <BaseButton
      label="Sing Up"
      type="submit"
      :aria-disabled="errorsFields.isInvalidForm"
      :disabled="errorsFields.isInvalidForm"
    />
  </form>
</template>

<script lang="ts">
import { reactive, defineComponent, computed, toRefs } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { email, required, helpers, sameAs } from "@vuelidate/validators";

import BaseInput from "@/components/BaseInput.vue";
import BaseButton from "@/components/BaseButton.vue";

export default defineComponent({
  components: {
    BaseInput,
    BaseButton,
  },
  emits: ["onSubmit"],
  setup(_, { emit }) {
    const register = reactive({
      first_name: "",
      last_name: "",
      email: "",
      password: "",
      password_confirmation: "",
    });

    const requiredField = helpers.withMessage("Campo requerido", required);
    const emailField = helpers.withMessage("Correo invalido", email);
    const samePassword = helpers.withMessage(
      "Las contraseñas deben ser iguales",
      sameAs(register.password)
    );
    const rules = computed(() => ({
      first_name: { required: requiredField },
      last_name: { required: requiredField },
      email: { required: requiredField, email: emailField },
      password: { required: requiredField },
      password_confirmation: {
        required: requiredField,
        sameAsPassword: samePassword,
      },
    }));
    const errorsFields = computed(() => ({
      first_name: v$.value.first_name.$errors?.[0]?.$message ?? "",
      last_name: v$.value.last_name.$errors?.[0]?.$message ?? "",
      email: v$.value.email.$errors?.[0]?.$message ?? "",
      password: v$.value.password.$errors?.[0]?.$message ?? "",
      password_confirmation:
        v$.value.password_confirmation.$errors?.[0]?.$message ?? "",
      isInvalidForm: v$.value.$invalid,
    }));

    const v$ = useVuelidate(rules, toRefs(register), { $autoDirty: true });

    function handleOnSubmit() {
      emit("onSubmit", { ...register });
    }

    function handleTouch(field: keyof typeof register) {
      v$.value?.[field].$touch();
    }

    return {
      v$,
      register,
      handleTouch,
      errorsFields,
      handleOnSubmit,
    };
  },
});
</script>

<style lang="scss">
.form-container {
  height: 500px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</style>
