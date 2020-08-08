<template>
  <div class="home">
    <Button v-on:showPopUp="showPopUpCreate" />
    <transition>
      <ModalCreate
        v-if="isModalCreateVisible"
        v-on:closeModal="closeModalCreate"
        v-on:addBot="addNewBot"
        v-bind:title="'Describe a new bot'"
        v-bind:buttonTitle="'Add new bot'"
        v-bind:showModal="isModalCreateVisible"
      />
      <ModalCreate
        v-if="isModalEditVisible"
        v-on:closeModal="closeModalCreate"
        v-on:addBot="addNewBot"
        v-bind:title="'Edit bot info'"
        v-bind:botInfo="botToEdit"
        v-bind:buttonTitle="'Save changes'"
        v-bind:showModal="isModalEditVisible"
      />
    </transition>
    <h2
      class="home__heading"
      v-if="!botsList.length"
    >
      Press button to add new bot
    </h2>
    <BotsList
      v-bind:botsList="botsList"
      v-on:delete-bot="onDelete"
      v-on:onShowModalEdit="showModalEdit"
    />
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
      isModalEditVisible: false,
      botsList: [],
      botToEdit: null,
    };
  },
  methods: {
    showPopUpCreate() {
      this.isModalCreateVisible = true;
    },
    showModalEdit(botId) {
      this.isModalEditVisible = true;
      this.botToEdit = this.botsList.find((bot) => bot.id === botId);
    },
    closeModalCreate() {
      this.isModalCreateVisible = false;
      this.isModalEditVisible = false;
    },
    onDelete(botId) {
      this.botsList = this.botsList.filter((bot) => bot.id !== botId);
    },
    addNewBot(bot, modalTitle) {
      console.log(bot, modalTitle);
      if (modalTitle === 'Describe a new bot') {
        this.botsList = [...this.botsList, bot];
        this.isModalCreateVisible = false;
      } else if (modalTitle === 'Edit bot info') {
        this.botsList = this.botsList.map((currentBot) => {
          console.log(currentBot.id, bot.id);
          if (currentBot.id === bot.id) {
            return {
              id: bot.id,
              name: bot.name,
              descripton: bot.descripton,
              file: bot.file,
              image: bot.image,
              time: bot.time,
            };
          }

          return currentBot;
        });
      }
    },
  },
};
</script>
