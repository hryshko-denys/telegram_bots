<template>
  <div class="modal__field-wrapper">
    <label
      for="description"
      class="modal__label modal__label--text"
    >
      Description
    </label>
    <div
      class="modal__textarea-wrapper"
      v-bind:class="{ modal__description_error: descriptionError }"
    >
      <textarea
        name="description"
        class="modal__textarea"
        id="description"
        placeholder="Type a description here..."
        :value="description"
        @change="handleDescription"
        @blur="handleValidation"
      >
      </textarea>
    </div>
  </div>
</template>

<script>

export default {
  name: 'ModalTextarea',
  props: ['descriptionError', 'handleValidation', 'description'],
  methods: {
    handleDescription(event) {
      const { value } = event.target;
      this.$emit('handleDescription', value);
    },
  },
};
</script>

<style lang="scss">
@import "../../styles/variables";

.modal {

  &__field-wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;

    width: 100%;
  }

  &__label {
    position: relative;
    font-size: 1.5rem;
    font-weight: bold;

    cursor: pointer;
  }

  &__textarea-wrapper {
    position: relative;
    width: 40%;
    padding: 10px;

    border: 1px solid $blue;
    border-radius: 15px;
  }

  &__textarea {
    width: 100%;
  }

  &__description_error {
    border: 1px solid $tomatored;
  }

  &__description_error::after {
    content: 'Type correct description';
    position: absolute;
    top: calc(50% - 11px);
    left: -190px;
    display: block;

    color: $tomatored;
  }

  &__textarea::placeholder {
    font-family: 'Raleway', 'Arial', sans-serif;
  }

  &__textarea::placeholder {
    padding-top: 10px;
  }

  &__textarea {
    background-color: #FFFAF0;
  }
}
</style>
