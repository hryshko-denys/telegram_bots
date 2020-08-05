<template>
  <div
    class="modal__upload"
    @dragenter="onDragEnter"
    @dragleave="onDragLeave"
    @dragover.prevent
    @drop="onDrop"
    :class="{ modal__dragging: isDragging }"
  >
    <ModalUpload
      v-bind:images="images"
      v-on:changeInput="onChangeInput"
    />
    <ModalImages v-bind:images="images" v-bind:files="files" />
  </div>
</template>

<script>
import ModalUpload from './ModalUpload.vue';
import ModalImages from './ModalImages.vue';

export default {
  name: 'ModalDragAndDrop',
  components: {
    ModalUpload,
    ModalImages,
  },
  data() {
    return {
      isDragging: false,
      dragCount: 0,
      images: [],
      files: [],
    };
  },
  methods: {
    onChangeInput(files) {
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
// @import "../../styles/variables";

.modal {

  &__upload {
    position: relative;

    width: 100%;
    padding: 20px;

    border-radius: 10px;
    background-color: #87CEEB;
    transition: background-color 0.2s cubic-bezier(.4,0,.2,1);
    // opacity: 0.7;
  }

  &__dragging {
    background-color: #98FB98;
  }
}
</style>
