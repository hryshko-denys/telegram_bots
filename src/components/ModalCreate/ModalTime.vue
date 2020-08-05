<template>
  <div class="modal__date-wrapper">
    <label for="data" class="modal__label modal__label--date">
      Choose the date here
    </label>
    <date-picker
      class="modal__date"
      id="date"
      v-model="time"
      type="datetime"
      lang="eng"
      valueType="format"
      format="YYYY-MM-DD HH:hh:ss a"
      width="500"
      confirm
    >
    </date-picker>
  </div>
</template>

<script>
import DatePicker from 'vue2-datepicker';
import 'vue2-datepicker/index.css';

export default {
  name: 'ModalTime',
  components: {
    DatePicker,
  },
  data() {
    return {
      time: null,
    };
  },
  // methods: {
  //   closeModalCreate() {
  //     this.$emit('closeModal');
  //   },
  // },
};
</script>

<style lang="scss">
@import "../../styles/variables";

.modal {

  &__label {
    position: relative;
    font-size: 1.5rem;
    font-weight: bold;

    cursor: pointer;
  }

  &__label--date {
    cursor: auto;
  }

  &__date-wrapper {
    display: flex;
    justify-content: space-between;

    width: 100%;
  }
}
</style>
