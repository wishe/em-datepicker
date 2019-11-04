<template>
    <div class="em-datepickers">
      <DatePicker
        v-model="dateInput.from"
        ref="datepickerFrom"
        name="em-start"
        format="dd/MM/yyyy"
        :input-class="inputClass"
        :wrapper-class="wrapperClass"
        maximum-view="month"
        :language="languages.nbNO"
        @selected="openDatepickerTo()">
        <template v-slot:beforeCalendarHeader>
          <div class="em-datepicker-buttons">
            <div
              class="em-datepicker-button"
              @click="setThisWeek()">
              {{ strings.week[language] }}
            </div>
            <div
              class="em-datepicker-button"
              @click="setNextTenDays()">
              {{ strings.nextTen[language] }}
            </div>
            <div
              class="em-datepicker-button"
              @click="setThisMonth()">
              {{ strings.month[language] }}
            </div>
          </div>
        </template>
      </DatePicker>
      <DatePicker
        v-model="dateInput.to"
        ref="datepickerTo"
        name="em-end"
        format="dd/MM/yyyy"
        :input-class="inputClass"
        :wrapper-class="wrapperClass"
        maximum-view="month"
        :language="languages.nbNO">
      </DatePicker>
    </div>
</template>
<script>
import DatePicker from 'vuejs-datepicker';
import { en, nbNO } from 'vuejs-datepicker/dist/locale';


export default {
  name: 'emDatePicker',
  props: {
    value: Object,
    language: String,
    disabled: Array,
    inputClass: String,
    wrapperClass: String,

  },
  components: {
    DatePicker,
  },
  data() {
    return {
      dateInput: {
        from: undefined,
        to: undefined,
      },
      languages: {
        en,
        nbNO,
      },
      strings: {
        week: {
          en: 'This week',
          nbNO: 'Denne uken',
        },
        nextTen: {
          en: 'Next 10 days',
          nbNO: 'Neste 10 dager',
        },
        month: {
          en: 'This month',
          nbNO: 'Denne måneden',
        },
      },
    };
  },
  computed: {
    selectedLanguage() {
      return this.languages[this.language];
    },
  },
  methods: {
    // Check if date is a Date object or a Unix Timestamp before we set it
    setDates() {
      if (this.value.from instanceof Date) {
        this.dateInput.from = this.value.from;
      } else {
        this.dateInput.from = new Date(this.value.from);
      }

      if (this.value.to instanceof Date) {
        this.dateInput.to = this.value.to;
      } else {
        this.dateInput.to = new Date(this.value.to);
      }
    },
    // Set disabled dates based on props
    setDisabledDates() {
    },
    setThisWeek() {
      const date = new Date();
      this.dateInput.from = new Date(date.setDate(date.getDate() - date.getDay()));
      this.dateInput.to = new Date(date.setDate(date.getDate() - date.getDay() + 6));
    },
    setNextTenDays() {
      const date = new Date();
      this.dateInput.from = new Date();
      this.dateInput.to = new Date(date.setDate(date.getDate() + 10));
    },
    setThisMonth() {
      const date = new Date();
      this.dateInput.from = new Date(date.getFullYear(), date.getMonth(), 1);
      this.dateInput.to = new Date(date.getFullYear(), date.getMonth() + 1, 0);
    },
    openDatepickerTo() {
      this.$refs.datepickerTo.showCalendar();
    },
  },
  watch: {
    'dateInput.from': function (val) {
      if (val > this.dateInput.to) {
        this.dateInput.to = val;
      }
    },
    'dateInput.to': function (val) {
      if (val < this.dateInput.from) {
        this.dateInput.from = val;
      }
    },
    dateInput: {
      handler() {
        this.$emit('input', this.dateInput);
      },
      deep: true,
    },
  },
  beforeMount() {
    this.setDates();
    this.setDisabledDates();
  },
};
</script>
<style lang="scss" scoped>
  .em-datepickers {
    display: inline-block;
    .vdp-datepicker {
      display: inline-block;
      margin-bottom: 0;
    }
    .vdp-datepicker:first-child {
      margin-right: 1rem;
    }
    .em-datepicker-buttons {
      display: flex;
      justify-content: space-around;
      margin: .5rem .25rem .5rem .25rem;
      .em-datepicker-button {
        padding: .25rem;
        border: 1px solid #EEEEEE;
        font-size: .8rem;
        &:hover {
          cursor: pointer;
          background-color: #EBEBEB;
        }
      }
    }
  }
</style>
