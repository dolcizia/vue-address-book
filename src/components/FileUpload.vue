<template>
  <div class="file-upload">
    <input type="file" id="uploader" @change="onChange" />
    <label class="btn btn-dark" for="uploader"
      ><i class="fas fa-file-upload"></i>Upload Image</label
    >
  </div>
</template>

<script>
  export default {
    name: 'FileUpload',
    methods: {
      onChange(e) {
        this.$emit('change', e.target.files[0]);
      }
    }
  };
</script>

<style lang="scss" scoped>
  @import '../styles/variables.scss';

  input[type='file'] {
    opacity: 0 !important;
    position: absolute;
    pointer-events: none;
    width: 1px;
    height: 1px;
  }

  i {
    margin-right: $space-sm;
  }
</style>
