<template>
  <div class="bots">
    <ol class="bots__list">
      <li
        class="bots__item"
        v-for="bot in botsList"
        v-bind:key="bot.id"
      >
        <BotItem
          v-bind:bot="bot"
          v-on:delete-bot="onDelete"
          v-on:onShowModalEdit="showModalEdit"
        />
      </li>
    </ol>
  </div>
</template>

<script>
import BotItem from './BotItem.vue';

export default {
  name: 'BotsList',
  components: {
    BotItem,
  },
  props: ['botsList'],
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
@import "../styles/extends";

.bots {
  max-width: 35%;
  margin: 0 auto;

  &__list {
  margin: 1.75rem 0;
  padding-left: 1rem;

  counter-reset: gradient-counter;
  list-style: none;
  }

  &__item {
    position: relative;
    display: grid;
    place-items: center;

    margin-top: 2rem;
    min-height: 3rem;
    padding: 1rem 1rem 1rem 3rem;

    background: #fafafa;
    border-radius: 0 0.5rem 0.5rem 0.5rem;
    counter-increment: gradient-counter;

    @extend %boxshadow;
  }

  &__item::before,
  &__item::after {
    content: '';
    position: absolute;
    left: -1rem;
    top: -1rem;

    width: 3rem;
    height: 3rem;

    background: linear-gradient(135deg, $blue 0%,$green 100%);
    border-radius: 1rem 1rem 0 1rem;
    overflow: hidden;
  }
  &__item::before {
    content: counter(gradient-counter);
    display: flex;
    justify-content: flex-end;
    align-items: flex-end;
    z-index: 1;
    padding: 0.125em 0.25em;

    color: $black;
    font: 900 1.5em/1 'Montserrat';
    @extend %boxshadow;
  }
}
</style>
