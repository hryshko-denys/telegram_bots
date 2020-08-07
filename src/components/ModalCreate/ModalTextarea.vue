<template>
  <div class="modal__field-wrapper">
    <label
      for="description"
      class="modal__label modal__label--text"
    >
      Description
    </label>
    <textarea
      class="modal__textarea"
      id="description"
      placeholder="Type a description here..."
      @change="handleDescription"
    >
    </textarea>
  </div>
</template>

<script>

export default {
  name: 'ModalTextarea',
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

  &__textarea {
    padding: 10px;
    border: 1px solid $blue;
    border-radius: 15px;
    width: 45%;
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
