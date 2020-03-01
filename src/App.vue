<template>
  <div id="app">
    <modal v-if="!loggedIn">
      <login @login="login" />
    </modal>
    <div v-else class="main__content">
      <navbar :user="user" @toggle="toggleSettings" />

      <modal v-if="showSettings">
        <settings :user="user" @update="updateUser" @toggle="toggleSettings" />
      </modal>

      <modal v-if="showContactForm">
        <add-contact-form
          @toggle="toggleContactForm"
          @add="addContact"
          :nextId="computeId"
        />
      </modal>

      <div class="contact-area">
        <div class="contact-area__content">
          <contact-list
            v-if="contacts"
            :contacts="contacts"
            @toggle="toggleContactForm"
            @click="selectContact"
          />

          <div class="contact-details__wrapper">
            <contact-details
              v-if="selected"
              :contact="selected"
              @delete="deleteContact"
            />
            <div class="message" v-else>
              Please select a contact to view details
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Login from './components/Login';
  import Settings from './components/Settings';
  import Navbar from './components/Navbar';
  import ContactList from './components/ContactList';
  import AddContactForm from './components/AddContactForm';
  import ContactDetails from './components/ContactDetails';
  import Modal from './components/Modal';
  import { contacts } from './contacts';

  export default {
    name: 'App',
    components: {
      Login,
      Settings,
      ContactList,
      ContactDetails,
      AddContactForm,
      Navbar,
      Modal
    },
    data() {
      return {
        loggedIn: false,
        user: '',
        contacts: contacts,
        showSettings: false,
        showContactForm: false,
        selected: ''
      };
    },
    computed: {
      computeId() {
        if (this.contacts.length < 1) {
          return 0;
        }

        let last = this.contacts[this.contacts.length - 1].id;

        return (last += 1);
      }
    },
    methods: {
      login(user) {
        this.user = user;
        this.loggedIn = true;
      },
      updateUser(user) {
        this.user = user;
        this.showSettings = false;
      },
      toggleSettings() {
        this.showSettings = !this.showSettings;
      },
      toggleContactForm() {
        this.showContactForm = !this.showContactForm;
      },
      addContact(newContact) {
        contacts.push(newContact);

        this.toggleContactForm();
      },
      selectContact(contact) {
        this.selected = contact;
      },
      deleteContact(id) {
        this.contacts = this.contacts.filter(contact => contact.id !== id);
        this.selected = '';
      }
    }
  };
</script>

<style lang="scss">
  @import './styles/variables.scss';
  * {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
  }
  .row {
    background: $light;
    border-bottom: 1px solid $gray;

    &:last-of-type {
      border-bottom: none;
    }
  }
  input {
    border: 1px solid $primary;
  }
  .contact-area {
    margin-top: 100px;
    padding: 0 $space;

    @media (min-width: $medium) {
      justify-content: center;
      margin: 70px auto 0 auto;
      padding: 0;
      width: 568px;
      box-sizing: border-box;
    }

    .contact-area__content {
      border: $border;
      padding: $space;
      margin: 120px auto $space-lg auto;
      width: 100%;

      @media (min-width: $medium) {
        display: flex;
      }

      .contact-details__wrapper {
        text-align: center;

        @media (min-width: $medium) {
          width: 217px;
        }
      }
    }
  }
</style>
