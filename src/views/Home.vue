<template>
  <div class="home">
    <Button v-on:showPopUp="showPopUpCreate" />
    <ModalCreate
      v-if="isModalCreateVisible"
      v-on:closeModal="closeModalCreate"
      v-on:addBot="addNewBot"
    />
    <BotsList v-bind:botsList="botsList" v-on:delete-bot="onDelete" />
  </div>
</template>

<script>
import Button from '@/components/Button.vue';
import ModalCreate from '@/components//ModalCreate/ModalCreate.vue';
import BotsList from '@/components/BotsList.vue';

export default {
  name: 'Home',
  components: {
    Button,
    ModalCreate,
    BotsList,
  },
  data() {
    return {
      isModalCreateVisible: false,
      botsList: [
        {
          name: 'Weather',
          id: 1,
          descripton: 'Get actual weather',
          file: 'starwars.jpg',
          image: '...',
          time: '2020-08-25 17:05:05 pm',
        },
        {
          name: 'News',
          id: 2,
          descripton: 'Get actual news',
          file: 'yalantis.png',
          image: '...',
          time: '2020-08-25 17:05:05 pm',
        },
      ],
    };
  },
  methods: {
    showPopUpCreate() {
      this.isModalCreateVisible = true;
    },
    closeModalCreate() {
      this.isModalCreateVisible = false;
    },
    onDelete(botId) {
      this.botsList = this.botsList.filter((bot) => bot.id !== botId);
    },
    addNewBot(bot) {
      this.botsList = [...this.botsList, bot];
    },
  },
};
</script>
