<template>
  <div class="contact-details">
    <h2 class="contact__name">{{ formatName }}</h2>
    <div class="image-container">
      <img
        v-if="!contact.blob"
        :src="require(`@/assets/${contact.image}`)"
        alt=""
      />
      <img v-else-if="contact.blob" :src="contact.blob" alt="" />
    </div>

    <em>{{ contact.company }}</em>
    <phone-number
      v-for="(number, index) in contact.numbers"
      :number="number"
      :key="index"
      :class="{ primary: number.num === contact.primary.num }"
    />
    <ui-button :data="contact" @click="$emit('delete', contact.id)" color="red"
      >Delete Contact</ui-button
    >
  </div>
</template>

<script>
  import PhoneNumber from './PhoneNumber';
  import UiButton from './UiButton';
  export default {
    name: 'ContactDetails',
    props: ['contact'],
    components: {
      PhoneNumber,
      UiButton
    },
    computed: {
      formatName() {
        const { title, first, last } = this.contact;

        return `${title} ${first} ${last}`;
      }
    },
    methods: {
      deleteContact(id) {
        console.log(id);
      }
    }
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';

  .contact-details {
    @media (min-width: $medium) {
      padding: $space;
      height: 307px;
      overflow: scroll;
      border: 1px solid $dark;
      margin-left: $space;
    }

    .btn {
      margin-top: $space;
    }

    @media (min-width: $medium) {
      img {
        width: 100%;
        height: auto;
      }
    }
  }
</style>
