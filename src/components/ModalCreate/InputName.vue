<template>
  <div class="modal__field-wrapper">
    <label
      for="name"
      class="modal__label modal__label--text"
    >
      Name
    </label>
    <input
      class="modal__text"
      type="text"
      id="name"
      placeholder="Type a name here..."
    >
  </div>
</template>

<script>

export default {
  name: 'InputName',
  components: {
  },
  // methods: {
  //   closeModalCreate() {
  //     this.$emit('closeModal');
  //   },
  // },
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

  &__text {
    padding: 10px;
    border: 1px solid $blue;
    border-radius: 15px;
    width: 45%;
  }

  &__text::placeholder {
    font-family: 'Raleway', 'Arial', sans-serif;
  }
}
</style>
