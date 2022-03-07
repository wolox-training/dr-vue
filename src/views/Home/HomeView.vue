<template>
  <main class="main">
    <section class="main-container">
      <div class="container">
        <img src="../../assets/wolox-logo.png" alt="wolox-logo" />
        <RegisterForm @onSubmit="handleSubmit" />
      </div>
    </section>
  </main>
</template>

<script lang="ts">
import RegisterForm from "./components/RegisterForm.vue";
type register = {
  first_name: string;
  last_name: string;
  email: string;
  password: string;
  password_confirmation: string;
  locale: string;
};

export default {
  components: {
    RegisterForm,
  },
  setup() {
    function handleSubmit(args: register) {
      console.log("amaaaaaaaaa", args);
    }

    return { handleSubmit };
  },
};
</script>

<style lang="scss" scoped>
.main {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.main-container {
  background-color: #ececec;
  border-top: 5px solid #00adee;
  flex-direction: column;
  min-height: 620px;
  padding: 15px;
  width: 300px;
}
</style>
