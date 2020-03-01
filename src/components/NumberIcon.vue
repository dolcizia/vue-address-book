<template>
  <i class="number-icon fas" :class="classes" @click="$emit('type', type)"></i>
</template>

<script>
  export default {
    name: 'NumberIcon',
    props: ['type', 'selected'],
    computed: {
      classes() {
        return [
          { 'fa-home': this.type === 'home' },
          { 'fa-mobile-alt': this.type === 'cell' },
          { 'fa-briefcase': this.type === 'work' },
          { active: this.selected === this.type }
        ];
      }
    }
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';
  .number-icon {
    &.selectable {
      color: $gray;
      opacity: 0.7;
    }

    &.active {
      color: $dark;
      opacity: 1;
    }
  }
</style>
