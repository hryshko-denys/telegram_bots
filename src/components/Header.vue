<template>
  <div class="nav" id="nav">
    <div class="nav__wrapper">
      <h1 class="nav__heading">Telegram bots</h1>
      <img
        class="nav__image"
        src="../assets/telegram.png"
        alt="Telegram"
      >
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
};
</script>

<style lang="scss">
@import "../styles/variables";

.nav {
  display: grid;
  place-items: center;
  border-bottom: 1px solid #FFA07A;

  width: 100%;
  min-height: 100px;
  margin-bottom: 80px;
  background-color: #F0F8FF;

  &__wrapper {
    display: flex;
    width: 400px;

    font-size: 3rem;
  }

  &__heading {
    color: $blue;
    margin-right: 20px;
  }

  &__image {
    width: 50px;
    height: 50px;
  }
}
</style>
