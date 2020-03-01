<template>
  <div class="number-group">
    <div class="number-group__numbers">
      <phone-number
        class="phone-number"
        :class="{ primary: primary.num === number.num }"
        v-for="(number, index) in numbers"
        :key="index"
        :number="number"
        :index="index"
      />
    </div>

    <div class="add-number">
      <input
        type="tel"
        v-model="tempNumber"
        required
        placeholder="eg: 123-456-7890"
      />
      <div class="icon-group">
        <number-icon
          type="home"
          :selected="selectedType"
          @type="setType"
          :class="classes"
        />
        <number-icon
          type="cell"
          :selected="selectedType"
          @type="setType"
          :class="classes"
        />
        <number-icon
          type="work"
          :selected="selectedType"
          @type="setType"
          :class="classes"
        />
      </div>

      <ui-button color="dark" @click="addNumber">+</ui-button>
    </div>
  </div>
</template>

<script>
  import PhoneNumber from './PhoneNumber';
  import UiButton from './UiButton';
  import NumberIcon from './NumberIcon';
  export default {
    name: 'NumberGroup',
    components: {
      PhoneNumber,
      UiButton,
      NumberIcon
    },
    props: ['numbers', 'primary'],
    data() {
      return {
        tempNumber: '',
        type: '',
        selectedType: 'home'
      };
    },
    computed: {
      classes() {
        return [{ active: this.activeType === this.type }, 'selectable'];
      }
    },
    methods: {
      addNumber() {
        if (this.tempNumber !== '') {
          const newNumber = {
            num: this.tempNumber,
            type: this.selectedType
          };

          this.$emit('add', newNumber);

          this.tempNumber = '';
        }
      },
      setType(selected) {
        this.selectedType = selected;
      }
    }
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';
  .number-group {
    padding-bottom: $space-sm;

    .number-group__numbers {
      margin-bottom: $space;
    }
  }
  .phone-number {
    cursor: pointer;
    display: flex;
    align-items: center;
    padding: $space-sm $space;
    justify-content: space-between;

    &:before {
      content: '';
    }

    &.primary:before {
      content: 'primary';
      text-transform: uppercase;
      font-size: 10px;
      color: $green;
      letter-spacing: 0.2px;
    }
  }

  .add-number {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;

    input {
      width: 50%;
    }

    .icon-group {
      width: 25%;
      display: flex;
      justify-content: space-around;
    }
  }
</style>
