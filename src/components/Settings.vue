<template>
  <div class="settings">
    <h1>Settings</h1>
    <div class="form">
      <label for="username">Update Username</label>
      <input type="text" v-model="username" name="username" required />

      <div class="button-group">
        <ui-button color="light" @click="$emit('toggle')">
          Cancel
        </ui-button>
        <ui-button color="dark" @click="$emit('update', username)">
          Save
        </ui-button>
      </div>
    </div>
  </div>
</template>

<script>
  import UiButton from './UiButton';
  export default {
    name: 'Settings',
    props: ['user'],
    components: {
      UiButton
    },
    data() {
      return {
        username: this.user
      };
    }
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';
  .form {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: $space;

    input {
      margin: $space 0;
      min-height: 24px;
    }

    .button-group {
      display: flex;
      flex-direction: row;

      .btn {
        margin-bottom: 0;

        &:first-of-type {
          margin-right: $space-sm;
        }
      }
    }
  }
</style>
