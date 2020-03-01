<template>
  <div class="contact-list">
    <div class="contact-list__header">
      <h2>Contacts</h2>
      <ui-button color="dark" @click="$emit('toggle')">Add Contact</ui-button>
    </div>
    <div class="contact-list__contacts">
      <contact
        v-for="(contact, index) in contacts"
        :key="index"
        :contact="contact"
      />
    </div>
  </div>
</template>

<script>
  import Contact from './Contact';
  import UiButton from './UiButton';
  export default {
    name: 'ContactList',
    props: ['contacts'],
    components: {
      Contact,
      UiButton
    }
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';
  .contact-list {
    width: 100%;

    @media (min-width: $medium) {
      width: 60%;
      border-right: $border;
      padding-right: $space;
    }

    .contact-list__header {
      display: flex;
      justify-content: space-between;
      padding: $space 0;
    }

    .contact-list__contacts {
      height: 250px;
      overflow: scroll;
      border: 1px solid $dark;
      margin-bottom: $space;

      @media (min-width: $medium) {
        margin-bottom: 0;
      }
    }
  }
</style>
