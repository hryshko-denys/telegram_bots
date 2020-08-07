<template>
  <div class="modal__buttons">
    <button
      @click="onSubmit"
      type="button"
      class="modal__button modal__button--add"
    >
      Add new Bot
    </button>
    <button
      type="button"
      class="modal__button modal__button--close"
      @click="closeModalCreate"
    >
      Close
    </button>
  </div>
</template>

<script>

export default {
  name: 'ModalButtons',
  components: {
  },
  methods: {
    closeModalCreate() {
      this.$emit('closeModal');
    },
    onSubmit() {
      this.$emit('handleSubmit');
    },
  },
};
</script>

<style lang="scss">
@import "../../styles/variables";

.modal {

   &__buttons {
    display: flex;
    justify-content: space-evenly;

    width: 100%;
  }

  &__button {
    padding: 15px;

    font-size: 1.5rem;
    font-weight: bold;
    color: #fff;

    border: none;
    border-radius: 20px;

    transition: opacity 0.2s cubic-bezier(.4,0,.2,1);
  }

  &__button:hover {
    opacity: 0.7;
  }

  &__button--add {
    background: #7DECAD;
    background: linear-gradient(to bottom right, #7DECAD, #4CE2E6);
  }

  &__button--close {
    background: #EC7D7D;
    background: linear-gradient(to bottom right, #EC7D7D, #E64CE1);
  }

  &__button--close {
    background-color: red;
  }
}
</style>
