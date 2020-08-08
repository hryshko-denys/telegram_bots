<template>
  <div
    class="bots__content"
  >
    <span
      class="bots__name"
      @click="showModalEdit(bot.id)"
    >
      {{bot.name}}
    </span>
    <img :src="bot.image[0]" :alt="`${bot.name} image`" class="bots__image">
    <div class="bots__container" @click="onDelete(bot.id)">
      <div class="bots__left"></div>
      <div class="bots__right"></div>
      <label class="bots__close">close</label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BotItem',
  props: ['bot'],
  methods: {
    onDelete(botId) {
      this.$emit('delete-bot', botId);
    },
    showModalEdit(botId) {
      this.$emit('onShowModalEdit', botId);
    },
  },
};
</script>

<style lang="scss">
@import "../styles/variables";

.bots {
  &__name {
    font-size: 2rem;
    color: #FFA07A;

    cursor: pointer;
  }

  &__container {
    position: absolute;
    top: calc(50% - 30px);
    right: 0;

    width: 50px;
    height: 50px;
    cursor: pointer;
  }

  &__left,
  &__right {
    position: absolute;
    width: 50px;
    height: 4px;
    margin-top: 24px;

    background-color: $blue;
    border-radius: 2px;
    transition: all .3s ease-in;
  }

  &__left {
    transform: rotate(45deg);
  }

  &__right {
    transform: rotate(-45deg);
  }

  &__close {
    position: absolute;
    bottom: -10px;
    right: calc(50% - 21px);

    color: $blue;
    font-size: .6em;
    text-transform: uppercase;
    letter-spacing: 2px;
    transition: all .3s ease-in;
    opacity: 0;
  }

  &__container:hover &__left,
  &__container:hover &__right {
    background-color: $tomatored;
  }

  &__container:hover &__left {
    transform: rotate(-45deg);
  }
  &__container:hover &__right {
    transform: rotate(45deg);
  }
  &__container:hover &__close {
    opacity: 1;
  }

  &__image {
    position: absolute;
    top: calc(50% - 30px);
    left: 100px;
    max-height: 60px;
    max-width: 60px;
    object-fit: contain;
    background-size: cover;
  }
}

</style>
