<template>
  <TitleBlock title="Прогноз погоды" />
  <CurrentWeather ></CurrentWeather>
</template>

<script>
import TitleBlock from './components/TitleBlock.vue';
import CurrentWeather from './components/CurrentWeather.vue';

export default {
  name: 'App',
  components: {
    TitleBlock,
    CurrentWeather
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
