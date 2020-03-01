<template>
  <div class="add-contact">
    <div class="profile-image">
      <file-upload @change="onFileChange" />

      <div class="upload-preview" v-if="image.length > 0">
        <img v-if="image !== 'placeholder.jpg'" :src="image" alt="image" />
      </div>
    </div>

    <div class="main-fields">
      <input type="text" v-model="title" name="title" placeholder="Title" />
      <input
        type="text"
        v-model="first"
        name="first"
        placeholder="First Name"
        required
      />
      <input
        type="text"
        v-model="last"
        name="last"
        placeholder="Last Name"
        required
      />
      <input
        type="text"
        v-model="company"
        name="company"
        placeholder="Company"
      />
    </div>

    <div class="number-group__wrapper">
      <number-group
        @add="addNumber"
        :numbers="numbers"
        @primary="setPrimary"
        :primary="primary"
      />
    </div>

    <div class="error-container">
      <small class="error">{{ error }}</small>
    </div>

    <div class="button-group">
      <ui-button color="light" @click="$emit('toggle')">
        Cancel
      </ui-button>

      <ui-button color="dark" @click="addContact" type="submit">
        Add Contact
      </ui-button>
    </div>
  </div>
</template>

<script>
  import FileUpload from './FileUpload';
  import UiButton from './UiButton';
  import NumberGroup from './NumberGroup';

  export default {
    name: 'AddContactForm',
    components: {
      FileUpload,
      UiButton,
      NumberGroup
    },
    props: ['nextId'],
    data() {
      return {
        image: '',
        blob: '',
        title: '',
        first: '',
        last: '',
        company: '',
        numbers: [],
        primary: '',
        error: ''
      };
    },
    methods: {
      onFileChange(files) {
        this.image = URL.createObjectURL(files);
      },
      addNumber(number) {
        this.numbers.push(number);

        if (this.numbers.length === 1) {
          this.primary = number;
        }
      },
      setPrimary(i) {
        this.primary = this.numbers[i];
      },
      addContact() {
        if (this.image === '') {
          this.image = 'placeholder.jpg';
        }

        if (
          this.first === '' ||
          this.last === '' ||
          this.numbers.length === 0
        ) {
          this.error = 'Enter first name, last name & phone number';
        } else {
          this.error = '';
        }

        const contact = {
          id: this.nextId,
          blob: this.image,
          title: this.title,
          first: this.first,
          last: this.last,
          company: this.company,
          numbers: this.numbers,
          primary: this.primary
        };

        if (!this.error) {
          this.$emit('add', contact);
        }
      }
    }
  };
</script>

<style lang="scss">
  @import '../styles/variables.scss';
  .add-contact {
    width: 100%;

    @media (min-width: $medium) {
      display: grid;
      grid-template-columns: 1fr 2fr;
      grid-template-rows: auto;
      grid-template-areas: 'upload form' 'buttons numbers' 'buttons error';
      grid-column-gap: $space-lg;
    }

    input {
      height: 25px;
      margin: $space-sm 0;
      padding-left: $space;
    }

    .main-fields {
      display: flex;
      flex-direction: column;
      margin: $space 0;

      @media (min-width: $medium) {
        grid-area: form;
        margin-top: 0;
      }
    }
  }

  .profile-image {
    margin: $space 0;
    padding-bottom: $space;

    @media (min-width: $medium) {
      display: flex;
      align-items: center;
      flex-direction: column;
      padding-bottom: 0;
      grid-area: upload;
      margin-bottom: 0;

      label {
        font-size: 13px;
      }
    }

    .upload-preview img {
      max-width: 100px;
      max-height: 100px;
      margin-top: $space-lg;

      @media (min-width: $medium) {
        margin-top: $space;
      }
    }
  }

  .error-container {
    height: 20px;

    .error {
      color: $red;
    }

    @media (min-width: $medium) {
      grid-area: error;
    }
  }

  .number-group__wrapper {
    @media (min-width: $medium) {
      grid-area: numbers;
    }
  }

  .button-group {
    padding-top: $space;
    display: flex;
    justify-content: space-around;

    @media (min-width: $medium) {
      grid-area: buttons;
      padding-top: 0;
      flex-direction: column-reverse;
      justify-content: flex-end;

      .btn:first-of-type {
        margin-top: $space;
      }
    }
  }
</style>
