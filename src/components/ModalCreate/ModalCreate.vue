<template>
  <div class="modal__wrapper">
    <div class="modal">
      <h2 class="modal__heading">{{title}}</h2>
      <ModalForm
        v-on:closeModal="closeModalCreate"
        v-on:addBot="addNewBot"
        v-bind:botInfo="botInfo"
        v-bind:title="title"
        v-bind:buttonTitle="buttonTitle"
      />
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
  props: {
    title: {
      default: '',
    },
    botInfo: {
      default() {
        return [];
      },
    },
    buttonTitle: {
      default: '',
    },
  },
  methods: {
    closeModalCreate() {
      this.$emit('closeModal');
    },
    addNewBot(bot, modalTitle) {
      this.$emit('addBot', bot, modalTitle);
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
  // opacity: 0.9;

// &::after {
//   content: '';
//   position: absolute;
//   z-index: -1;
//   top: 0;
//   bottom: 0;
//   right: 0;
//   left: 0;
//   display: block;

//   width: 100%;
//   height: 100%;

//   background-color: #fff;
// }

&__wrapper {
  position: absolute;
  z-index: 0;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;

  display: flex;
  justify-content: center;
  align-items: center;

  background-color: #00BFFF;
  // opacity: 0.9;
}

&__heading {
  margin-bottom: 60px;

  font-size: 2.5rem;
  color: $blue;
  font-weight: bold;
}
}
</style>
