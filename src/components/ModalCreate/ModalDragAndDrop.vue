<template>
  <div
    class="modal__upload"
    @dragenter.prevent="onDragEnter"
    @dragleave.prevent="onDragLeave"
    @dragover.prevent
    @drop.prevent="onDrop"
    :class="{ modal__dragging: isDragging }"
  >
    <ModalUpload
      v-bind:currentImage="currentImage"
      v-on:changeImages="onChangeImages"
      v-bind:imageError="imageError"
    />
    <ModalImages
      v-bind:currentImage="currentImage"
      v-bind:currentFile="currentFile"
      v-on:changeImages="onChangeImages"
     />
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
  props: [
    'currentImage',
    'currentFile',
    'imageError',
  ],
  data() {
    return {
      isDragging: false,
      dragCount: 0,
    };
  },
  methods: {
    onChangeImages(files) {
      this.$emit('changeImages', files);
    },
    onDragEnter() {
      this.isDragging = true;
      this.dragCount += 1;
    },
    onDragLeave() {
      this.dragCount -= 1;
      if (this.dragCount <= 0) {
        this.isDragging = false;
      }
    },
    onDrop(event) {
      event.stopPropagation();

      this.isDragging = false;
      const { files } = event.dataTransfer;

      this.$emit('handleOnDrop', files);
    },
  },
};
</script>

<style lang="scss">

.modal {

  &__upload {
    position: relative;

    width: 100%;
    padding: 20px;

    border-radius: 10px;
    background-color: #87CEEB;
    transition: background-color 0.2s cubic-bezier(.4,0,.2,1);
  }

  &__dragging {
    background-color: #98FB98;
  }
}
</style>
