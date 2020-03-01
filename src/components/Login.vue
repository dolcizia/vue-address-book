<template>
  <div class="login">
    <h1>Please Login</h1>
    <form @submit.prevent="login">
      <input
        type="text"
        v-model="user"
        name="user"
        placeholder="Username"
        required
      />
      <input type="password" placeholder="Password" required />
      <ui-button color="light">Login</ui-button>
    </form>
  </div>
</template>

<script>
  import UiButton from './UiButton';
  export default {
    name: 'Login',
    components: {
      UiButton
    },
    data() {
      return {
        user: ''
      };
    },
    methods: {
      login() {
        this.$emit('login', this.user);
      }
    }
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';
  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: $space;

    input {
      margin: $space 0;
      min-height: 24px;
    }
  }
</style>
