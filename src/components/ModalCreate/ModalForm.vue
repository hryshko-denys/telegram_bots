<template>
  <form class="modal__form" @submit.prevent:="handleNewBot">
    <InputName
      v-on:handleName="onHandleName"
      v-bind:handleValidation="handleValidation"
      v-bind:nameError="errors.nameError"
      v-bind:name="currentName"
    />
    <ModalTextarea
      v-on:handleDescription="onHandleDescription"
      v-bind:handleValidation="handleValidation"
      v-bind:descriptionError="errors.descriptionError"
      v-bind:description="currentDescription"
     />
    <ModalDragAndDrop
      v-bind:currentImage="currentImage"
      v-bind:currentFile="currentFile"
      v-bind:imageError="errors.imageError"
      v-on:changeImages="onChangeImages"
      v-on:handleOnDrop="onDrop"
    />
    <ModalTime
      v-on:changeTime="handleTime"
      v-bind:timeError="errors.timeError"
      v-bind:currentTime="currentTime || 'choose time here'"
    />
    <ModalButtons
      v-on:closeModal="closeModalCreate"
      v-bind:isValid="isValid"
      v-bind:buttonTitle="buttonTitle"
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
  props: {
    botInfo: {
      default: [],
    },
    title: {
      default: 'Describe a bot',
    },
    buttonTitle: {
      default: '',
    },
  },
  data() {
    const name = this.botInfo.name || '';
    const descripton = this.botInfo.descripton || '';
    const file = this.botInfo.file || [];
    const image = this.botInfo.image || [];
    const time = this.botInfo.time || '';
    const { id } = this.botInfo;
    const { title } = this;
    return {
      currentName: name,
      currentDescription: descripton,
      currentFile: file,
      currentImage: image,
      currentTime: time,
      errors: {
        nameError: false,
        descriptionError: false,
        imageError: false,
        timeError: false,
      },
      isValid: true,
      currentId: id,
      modalTitle: title,
    };
  },
  methods: {
    closeModalCreate() {
      this.$emit('closeModal');
    },
    onHandleName(value) {
      this.currentName = value.replace(/^[\s]+|\s{2,}|\s+$/g, ''); // to handle spaces;
    },
    onHandleDescription(value) {
      this.currentDescription = value.replace(/^[\s]+|\s{2,}|\s+$/g, ''); // to handle spaces;
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

      this.currentFile = [file];

      const reader = new FileReader();

      this.currentImage.pop();
      reader.onload = (event) => this.currentImage.push(event.target.result);
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
      const validString = value.replace(/^[\s]+|\s{2,}|\s+$/g, '');

      if (validString.length < 3) {
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
        currentFile,
        currentImage,
        currentTime,
        modalTitle,
        currentId,
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

      if (!currentImage.length) {
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
        descripton: currentDescription,
        file: currentFile,
        image: currentImage,
        time: currentTime,
      };

      newBot.id = modalTitle === 'Describe a new bot'
        ? uuid()
        : currentId;

      this.$emit('addBot', newBot, modalTitle);
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
