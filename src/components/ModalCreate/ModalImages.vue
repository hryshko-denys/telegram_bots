<template>
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
</template>

<script>
export default {
  name: 'ModalImages',
  props: ['images', 'files'],
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
</style>
