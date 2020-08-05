<template>
  <div class="modal__wrapper">
    <div class="modal">
      <h2 class="modal__heading">Describe a new bot</h2>
      <ModalForm v-on:closeModal="closeModalCreate" />
    </div>
  </div>
</template>

<script>
import ModalForm from './ModalForm.vue';

export default {
  name: 'ModalCreate',
  components: {
    ModalForm,
  },
  methods: {
    closeModalCreate() {
      this.$emit('closeModal');
    },
  },
};
</script>

<style lang="scss">
@import "../../styles/variables";

  .modal {
      position: absolute;
      z-index: 3;

      width: 50%;
      padding: 50px;
      background-color: #FFFAF0;
      border-radius: 30px;
      // opacity: 1;

    &__wrapper {
      position: absolute;
      z-index: 2;
      top: 0;
      right: 0;
      left: 0;
      bottom: 0;

      display: flex;
      justify-content: center;
      align-items: center;

      background-color: #00BFFF;
      opacity: 1;
    }

    &__heading {
      margin-bottom: 60px;

      font-size: 2.5rem;
      color: $blue;
      font-weight: bold;
    }
  }
</style>
