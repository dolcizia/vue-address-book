<template>
  <div class="navbar__wrapper">
    <div class="navbar">
      <h1>Address Book</h1>
      <nav>
        <span>Hello, {{ user }}</span>
        <ui-button @click="$emit('toggle')" color="light">Settings</ui-button>
      </nav>
    </div>
  </div>
</template>

<script>
  import UiButton from './UiButton';
  export default {
    name: 'Navbar',
    props: ['user'],
    components: {
      UiButton
    }
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';
  .navbar__wrapper {
    position: fixed;
    width: 100vw;
    background: $gray;
    color: $primary;
    top: 0;

    .navbar {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      align-items: center;
      margin: $space;

      @media (min-width: $small) {
        flex-direction: row;
      }

      span {
        padding-right: $space;
      }
    }
  }
</style>
