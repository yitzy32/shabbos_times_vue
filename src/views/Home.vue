<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <input type="text" v-model="search">
    <button v-on:click="searchByZip()">Search</button> <br>
    <!-- <div v-if="selectedDay === []"> -->
      <h1>{{ selectedDay.date }}</h1>
      <p>Location: {{ selectedDay.name }}</p>
      <p>Mincha Gedola: {{ selectedDay.mincha_gedola }}</p>
      <p>Early Mincha: {{ selectedDay.mincha }}</p>
      <p>Plag HaMincha: {{ selectedDay.plag_hamincha }}</p>
      <p>Candel Lighting: {{ selectedDay.candle_lighting }}</p>
      <p>Sunset: {{ selectedDay.sunset }}</p>
      <p>Tzeis 50 MinUntes: {{ selectedDay.tzeis50min_fri_night }}</p>
      <p>Tzeis 72 Minutes: {{ selectedDay.tzeis72min_fri_night }}</p>
    <!-- </div> -->
    <a href="/calendar">Get the whole summer schedule</a>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      search: "",
      selectedDay: [],
    };
  },
  created: function () {},
  methods: {
    searchByZip: function () {
      var params = {
        search: this.search,
      };
      axios.get(`/api/zmanims?search=${this.search}`).then((response) => {
        console.log(response.data);
        this.selectedDay = response.data;
      });
    },
  },
};
</script>