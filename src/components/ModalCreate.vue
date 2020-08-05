<template>
  <div class="modal__wrapper">
    <div class="modal">
      <h2 class="modal__heading">Describe a new bot</h2>
      <form class="modal__form">
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
          >
          </textarea>
        </div>
        <div
          class="modal__upload"
          @dragenter="onDragEnter"
          @dragleave="onDragLeave"
          @dragover.prevent
          @drop="onDrop"
          :class="{ modal__dragging: isDragging }"
        >
          <div class="modal__drag-wrapper" v-show="!images.length">
            <h2 class="modal__label modal__label--upload">
              Drag your image here
            </h2>
            <label for="file" class="modal__label modal__label--button">
              Select a file
            </label>
            <input
              class="modal__download"
              type="file"
              id="file"
              value=null
              @change="onChangeInput"
              multiple
            >
          </div>
          <div class="modal__images images" v-show="images.length">
            <div class="images__list">
              <div
                class="images__wrapper"
                v-for="(image, index) in images"
                :key="index"
              >
                <img
                  :src="image"
                  alt="`Image ${index}`"
                  class="images__item"
                >
                <div class="images__details">
                  <span class="images__name" v-text="files[index].name"></span>
                  <span class="images__size" v-text="files[index].size"></span>
                </div>
              </div>
            </div>
            <div class="images__buttons">
                <button class="images__button">Select another file</button>
                <button class="images__button">Upload</button>
            </div>
          </div>
        </div>
        <div class="modal__date-wrapper">
          <label for="data" class="modal__label modal__label--date">
            Choose the date here
          </label>
          <date-picker
            class="modal__date"
            id="date"
            v-model="time"
            type="datetime"
            lang="eng"
            valueType="format"
            format="YYYY-MM-DD HH:hh:ss a"
            width="500"
            confirm
          >
          </date-picker>
        </div>
        <div class="modal__buttons">
          <button
            type="submit"
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
      </form>
    </div>
  </div>
</template>

<script>
import DatePicker from 'vue2-datepicker';
import 'vue2-datepicker/index.css';

export default {
  name: 'ModalCreate',
  components: {
    DatePicker,
  },
  data() {
    return {
      isDragging: false,
      dragCount: 0,
      images: [],
      files: [],
      time: null,
    };
  },
  methods: {
    closeModalCreate() {
      this.$emit('closeModal');
    },
    onChangeInput(event) {
      const { files } = event.target;

      [...files].forEach((file) => this.addImage(file));
    },
    onDragEnter(event) {
      event.preventDefault();
      this.isDragging = true;
      this.dragCount += 1;
    },
    onDragLeave(event) {
      event.preventDefault();

      this.dragCount -= 1;
      if (this.dragCount <= 0) {
        this.isDragging = false;
      }
    },
    onDrop(event) {
      event.preventDefault();
      event.stopPropagation();

      this.isDragging = false;
      const { files } = event.dataTransfer;

      [...files].forEach((file) => this.addImage(file));
    },
    addImage(file) {
      if (!file.type.match('image.*')) {
        return;
      }

      this.files = [...this.files, file];

      const reader = new FileReader();

      reader.onload = (event) => this.images.push(event.target.result);
      reader.readAsDataURL(file);
      console.log(this.files[0], this.images[0]);
    },
  },
};
</script>

<style lang="scss">
@import "../styles/variables";

  .modal {
      position: absolute;
      z-index: 3;

      width: 50%;
      padding: 16px;
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

    &__upload {
      position: relative;

      width: 100%;
      padding: 20px;

      border-radius: 10px;
      background-color: #87CEEB;
      transition: background-color 0.2s cubic-bezier(.4,0,.2,1);
      // opacity: 0.7;
    }

    &__heading {
      margin-bottom: 60px;

      font-size: 2.5rem;
      color: $blue;
      font-weight: bold;
    }

    &__form {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;

      height: 500px;
      padding: 10px;
    }

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

    &__label--upload {
      position: relative;

      width: 30%;
      font-size: 1.5rem;
      font-weight: bold;
    }

    &__label--button {
      align-self: flex-end;
      font-size: 1rem;
    }

    &__label--upload,
    &__label--date {
      cursor: auto;
    }

    &__label--button::after {
      position: absolute;
      content: '';
      top: -40px;
      right: calc(50% - 16px);
      display: block;
      width: 32px;
      height: 32px;

      background-image: url(../assets/upload.png);
      background-position: center;
      background-repeat: no-repeat;
    }

    &__text,
    &__textarea {
      padding: 10px;
      border: 1px solid $blue;
      border-radius: 15px;
    }

    &__text::placeholder,
    &__textarea::placeholder {
      font-family: 'Raleway', 'Arial', sans-serif;
    }

    &__textarea::placeholder {
      padding-top: 10px;
    }

    &__textarea {
      background-color: #FFFAF0;
    }

    &__drag-wrapper {
      display: flex;
      align-items: center;
      justify-content: space-between;
      min-height: 45px;
    }

    &__dragging {
      background-color: #98FB98;
    }

    &__heading-upload {
      width: 40%;
    }

    &__download {
      display: none;
    }

    &__drag-uploaded {
      display: flex;
      flex-wrap: wrap;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    &__date-wrapper {
      display: flex;
      justify-content: space-between;

      width: 100%;
    }

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
      // color: $blue;
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

    .images {
      display: flex;
      justify-content: space-between;
      width: 100%;

      &__list {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-evenly;
      }

      &__wrapper {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
      }

      &__wrapper:not(:last-child) {
        margin-right: 10px;
      }

      &__item {
        max-height: 75px;
        max-width: 75px;
        object-fit: contain;
      }

      &__buttons {
        display: flex;
        justify-content: flex-end;
        align-items: flex-end;
      }

      &__button {
        min-height: 3em;
        padding: 1em;
        margin: 0.5em;

        font-size: 0.5rem;
        background-color: $blue;
        border: none;
        border-radius: 3px;
        text-transform: uppercase;
        letter-spacing: 0.5em;
        transition: background-color 0.2s cubic-bezier(.4,0,.2,1);
      }

      &__button:last-child {
        margin-left: 20px;
      }

      &__button:hover {
        background-color: $softorange;
      }
    }
  }
</style>
