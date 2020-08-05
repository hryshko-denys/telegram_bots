<template>
  <form class="modal__form">
    <InputName />
    <ModalTextarea />
    <ModalDragAndDrop />
    <ModalTime />
    <ModalButtons v-on:closeModal="closeModalCreate" />
  </form>
</template>

<script>
import InputName from './InputName.vue';
import ModalTextarea from './ModalTextarea.vue';
import ModalDragAndDrop from './ModalDragAndDrop.vue';
import ModalTime from './ModalTime.vue';
import ModalButtons from './ModalButtons.vue';

export default {
  name: 'ModalForm',
  components: {
    InputName,
    ModalTextarea,
    ModalDragAndDrop,
    ModalTime,
    ModalButtons,
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

  &__form {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;

    height: 500px;
    padding: 10px;
  }
}
</style>
