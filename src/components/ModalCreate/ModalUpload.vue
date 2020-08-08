<template>
  <div class="modal__drag-wrapper" v-show="!currentImage.length">
    <h2
      class="modal__label modal__label--upload"
      v-bind:class="{ modal__image_error: imageError }"
    >
      Drag your image here
    </h2>
    <label
      for="file"
      class="modal__label modal__label--button"
      v-bind:class="{ modal__image_error: imageError }"
    >
      Select a file
    </label>
    <input
      name="image"
      class="modal__download"
      type="file"
      id="file"
      @change="onChangeImages"
      multiple
    >
  </div>
</template>

<script>
export default {
  name: 'ModalUpload',
  props: ['currentImage', 'imageError'],
  methods: {
    onChangeImages(event) {
      const { files } = event.target;
      this.$emit('changeImages', files);
    },
  },
};
</script>

<style lang="scss">
@import "../../styles/variables";

.modal {

  &__label {
    position: relative;
    font-size: 1.5rem;
    font-weight: bold;

    cursor: pointer;
  }

  &__label--upload {
    position: relative;

    width: 30%;
    font-size: 1.5rem;
    font-weight: bold;
  }

  &__label--button {
    align-self: flex-end;
    font-size: 1rem;
  }

  &__label--upload {
    cursor: auto;
  }

  &__label--button::after {
    position: absolute;
    content: '';
    top: -40px;
    right: calc(50% - 16px);
    display: block;
    width: 32px;
    height: 32px;

    background-image: url(../../assets/upload.png);
    background-position: center;
    background-repeat: no-repeat;
  }

  &__drag-wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    min-height: 55px;
  }

  &__download {
    display: none;
  }

  &__image_error {
    color: red;
  }
}
</style>
