<template>
  <div class="phone-number" @click="$parent.$emit('primary', index)">
    <span class="number">
      {{ number.num }}
      <number-icon class="number__icon" :type="number.type" :class="classes" />
    </span>
  </div>
</template>

<script>
  import NumberIcon from './NumberIcon';
  export default {
    name: 'PhoneNumber',
    props: ['number', 'index'],
    components: {
      NumberIcon
    },
    computed: {
      classes() {
        return [`number-${this.number.type}`];
      }
    }
  };
</script>

<style lang="scss">
  @import '../styles/variables.scss';
  .number-home {
    color: $indigo;
  }

  .number-cell {
    color: $pink;
  }

  .number-work {
    color: $blue;
  }

  .primary {
    border: 1px solid $green;
  }

  .number__icon {
    margin-left: $space;
    width: 20px;
  }
</style>
