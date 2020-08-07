<template>
  <div class="modal__images images" v-show="currentImages.length">
    <div class="images__list">
      <div
        class="images__wrapper"
        v-for="(image, index) in currentImages"
        :key="index"
      >
        <img
          :src="image"
          alt="`Image ${index}`"
          class="images__item"
        >
        <div class="images__details">
          <span class="images__name" v-text="currentFiles[index].name"></span>
        </div>
      </div>
    </div>
    <div class="images__another">
      <label for="file" class="modal__label modal__label--button">
        Select another file
      </label>
      <input
        class="modal__download"
        type="file"
        id="file"
        value=null
        @change="onChangeImages"
        multiple
      >
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalImages',
  props: ['currentImages', 'currentFiles'],
  methods: {
    onChangeImages(event) {
      const { files } = event.target;
      this.$emit('changeImages', files);
    },
  },
};
</script>

<style lang="scss">
@import "../../styles/variables";

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
    margin-bottom: 10px;
    object-fit: contain;
  }

  &__another {
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

  &__button:hover {
    background-color: $softorange;
  }
}
</style>
