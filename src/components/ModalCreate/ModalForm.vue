<template>
  <form class="modal__form" @submit.prevent:="handleNewBot">
    <InputName
      v-on:handleName="onHandleName"
      v-bind:handleValidation="handleValidation"
      v-bind:nameError="errors.nameError"
    />
    <ModalTextarea
      v-on:handleDescription="onHandleDescription"
      v-bind:handleValidation="handleValidation"
      v-bind:descriptionError="errors.descriptionError"
     />
    <ModalDragAndDrop
      v-bind:currentImages="currentImages"
      v-bind:currentFiles="currentFiles"
      v-bind:imageError="errors.imageError"
      v-on:changeImages="onChangeImages"
      v-on:handleOnDrop="onDrop"
    />
    <ModalTime
      v-on:changeTime="handleTime"
      v-bind:timeError="errors.timeError"
    />
    <ModalButtons
      v-on:closeModal="closeModalCreate"
      v-bind:isValid="isValid"
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
      errors: {
        nameError: false,
        descriptionError: false,
        imageError: false,
        timeError: false,
      },
      isValid: true,
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
      this.addImage(files[0]);
    },
    onDrop(files) {
      this.addImage(files[0]);
    },
    addImage(file) {
      if (!file.type.match('image.*')) {
        return;
      }

      this.currentFiles = [file];

      const reader = new FileReader();

      this.currentImages.pop();
      reader.onload = (event) => this.currentImages.push(event.target.result);
      reader.readAsDataURL(file);

      this.errors.imageError = false;
      this.isValid = true;
    },
    handleTime(time) {
      this.currentTime = time;
      this.errors.timeError = false;
      this.isValid = true;
    },
    handleValidation(event) {
      const { value, name } = event.target;
      const errorName = `${name}Error`;

      if (value.length < 3) {
        this.errors[errorName] = true;
        this.isValid = false;
      } else {
        this.errors[errorName] = false;
        this.isValid = true;
      }
    },
    handleNewBot(event) {
      event.preventDefault();
      const {
        currentName,
        currentDescription,
        currentFiles,
        currentImages,
        currentTime,
      } = this;

      if (currentName.length < 3) {
        this.errors.nameError = true;
        this.isValid = false;
        return;
      }

      if (currentDescription.length < 3) {
        this.errors.descriptionError = true;
        this.isValid = false;
        return;
      }

      if (!currentImages.length) {
        this.errors.imageError = true;
        this.isValid = false;
        return;
      }

      if (!currentTime) {
        this.errors.timeError = true;
        this.isValid = false;
        return;
      }

      const newBot = {
        name: currentName,
        id: uuid(),
        descripton: currentDescription,
        file: currentFiles[0],
        image: currentImages[0],
        time: currentTime,
      };

      this.$emit('addBot', newBot);
    },
  },
};
</script>

<style lang="scss">
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
