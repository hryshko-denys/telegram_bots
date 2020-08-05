<template>
  <div class="home">
    <Button v-on:showPopUp="showPopUpCreate" />
    <ModalCreate
      v-if="isModalCreateVisible"
      v-on:closeModal="closeModalCreate"
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
          img: '1.jpg',
          date: '14.07.2020',
        },
        {
          name: 'News',
          id: 2,
          descripton: 'Get actual news',
          img: '2.jpg',
          date: '15.07.2020',
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
  },
};
</script>
