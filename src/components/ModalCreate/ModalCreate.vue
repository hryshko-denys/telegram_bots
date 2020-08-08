<template>
  <div class="modal__wrapper">
  <transition appear>
    <div
      class="modal__overlay"
      v-if="showModal"
      @click="closeModalCreate"
      >
    </div>
  </transition>
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
    showModal: {
      default: false,
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
  position: fixed;
  z-index: 3;

  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  width: 100%;
  max-width: 900px;
  padding: 50px;
  background-color: #FFFAF0;
  border-radius: 30px;

  &__overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 2;
    background-color: rgba(0, 0, 0, 0.3);
  }

  &__wrapper {
    position: absolute;
    z-index: 1;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__heading {
    margin-bottom: 60px;

    font-size: 2.5rem;
    color: $blue;
    font-weight: bold;
  }
}

.v-enter-active,
.v-leave-active {
 transition: opacity .5s;
}

.v-enter,
.v-leave-active {
 opacity: 0;
}
</style>
