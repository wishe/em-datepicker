<template>
  <div id="app">
    <emDatePicker
      v-model="date"
      :language="language">
    </emDatePicker>
  </div>
</template>

<script>
import emDatePicker from './components/emDatePicker.vue';

export default {
  name: 'app',
  components: {
    emDatePicker,
  },
  data() {
    return {
      date: {
        from: '2019-01-01T22:09:39+0000',
        to: '2019-12-31T22:09:39+0000',
      },
      language: 'nbNO',
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
