<template>
  <div class="modal__mask">
    <div class="modal__window">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Modal'
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';
  .modal__mask {
    background: rgba(0, 0, 0, 0.75);
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;

    .modal__window {
      background: $white;
      display: flex;
      flex-direction: column;
      border: $border;
      padding: $space-lg;
      align-items: center;
      text-align: center;
      max-width: 100%;

      @media (max-width: $small) {
        margin: $space;
        max-width: 100%;
      }

      @media (min-width: $medium) {
        max-width: 50vw;
        margin: 150px auto;
      }
    }
  }
</style>
