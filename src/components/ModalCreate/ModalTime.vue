<template>
  <div class="modal__date-wrapper">
    <label
      for="data"
      class="modal__label modal__label--date"
      v-bind:class="{ modal__time_error: timeError }"
    >
      Choose the date here
    </label>
    <date-picker
      class="modal__date"
      id="date"
      v-model="time"
      @change="handleTime"
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
  props: ['timeError'],
  data() {
    return {
      time: null,
    };
  },
  methods: {
    handleTime() {
      const { time } = this;
      console.log(time);
      this.$emit('changeTime', time);
    },
  },
};
</script>

<style lang="scss">
@import "../../styles/variables";

.modal {

   &__date-wrapper {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }

  &__label {
    position: relative;
    font-size: 1.5rem;
    font-weight: bold;

    cursor: pointer;
  }

  &__time_error {
    color: red;
  }
}
</style>
