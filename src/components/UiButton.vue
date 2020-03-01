<template>
  <button class="btn" :class="classes" @click="$emit('click', data)">
    <slot></slot>
  </button>
</template>

<script>
  export default {
    name: 'UiButton',
    props: ['color', 'onClick', 'data'],
    computed: {
      classes() {
        return [`btn-${this.color}`];
      }
    }
  };
</script>

<style lang="scss">
  @import '../styles/variables.scss';
  .btn {
    cursor: pointer;
    border: none;
    border-radius: 0;
    text-transform: uppercase;
    padding: $space ($space * 2);

    &.btn-light {
      background: $lighter;

      &:hover {
        background: $light;
      }
    }

    &.btn-dark {
      color: $light;
      background: $dark;

      &:hover {
        background: $primary;
      }
    }

    &.btn-red {
      color: $primary;
      background: $red;

      &:hover {
        background: $red;
        opacity: 0.9;
      }
    }
  }
</style>
