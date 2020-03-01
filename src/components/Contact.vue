<template>
  <div class="contact-row row" @click="onClick(contact)">
    <h3>{{ contactInfo }}</h3>
    <div>
      <phone-number :number="primary" />
    </div>
  </div>
</template>

<script>
  import PhoneNumber from './PhoneNumber';
  export default {
    name: 'Contact',
    props: ['contact'],
    components: {
      PhoneNumber
    },
    data() {
      return {
        primary: this.contact.primary
      };
    },
    computed: {
      contactInfo() {
        const { title, first, last } = this.contact;
        return `${title} ${first} ${last}`;
      }
    },
    methods: {
      onClick(contact) {
        this.$parent.$emit('click', contact);
      }
    }
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';
  .contact-row {
    padding: $space;
  }
</style>
