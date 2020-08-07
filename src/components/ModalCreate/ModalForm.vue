<template>
  <form class="modal__form" @submit.prevent:="handleNewBot">
    <InputName v-on:handleName="onHandleName" />
    <ModalTextarea v-on:handleDescription="onHandleDescription" />
    <ModalDragAndDrop
      v-bind:currentImages="currentImages"
      v-bind:currentFiles="currentFiles"
      v-on:changeImages="onChangeImages"
      v-on:handleOnDrop="onDrop"
    />
    <ModalTime v-on:changeTime="handleTime" />
    <ModalButtons
      v-on:closeModal="closeModalCreate"
      v-on:handleSubmit="onSubmit"
    />
  </form>
</template>

<script>
import { uuid } from 'uuidv4';
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
  data() {
    return {
      currentName: '',
      currentDescription: '',
      currentFiles: [],
      currentImages: [],
      currentTime: '',
    };
  },
  methods: {
    closeModalCreate() {
      this.$emit('closeModal');
    },
    onHandleName(value) {
      this.currentName = value;
    },
    onHandleDescription(value) {
      this.currentDescription = value;
    },
    onChangeImages(files) {
      [...files].forEach((file) => this.addImage(file));
    },
    onDrop(files) {
      [...files].forEach((file) => this.addImage(file));
    },
    addImage(file) {
      if (!file.type.match('image.*')) {
        return;
      }

      this.currentFiles = [...this.currentFiles, file];

      const reader = new FileReader();
      reader.onload = (event) => this.currentImages.push(event.target.result);
      reader.readAsDataURL(file);
    },
    handleTime(time) {
      this.currentTime = time;
    },
    onSubmit() {
      const newBot = {
        name: this.currentName,
        id: uuid(),
        descripton: this.currentDescription,
        file: this.currentFiles[0],
        image: this.currentImages[0],
        time: this.currentTime,
      };

      this.$emit('addBot', newBot);
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
