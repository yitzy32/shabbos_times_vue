<template>
  <div class="calendar">
    <h1>{{ message }}</h1>
    <input type="text" v-model="search">
    <button v-on:click="getWholeCalendar()">Search</button>
    <div v-for="day in calendar" id="grid-container">
      <div id="grid-item">
        <h2>{{ day.date }}
        {{ day.name }}<br></h2>
        <b>Mincha Gedola </b>{{ day.mincha_gedola }}<br>
        <b>Plag HaMincha</b>{{ day.plag_hamincha }}<br>
        <b>Mincha: </b>{{ day.mincha }}<br>
        <b>Candle Lighting: </b>{{ day.candle_lighting }}<br>
        <b>Sunset: </b>{{ day.sunset }}<br>
        <b>Tzeis 50 Minutes</b>{{ day.tzeis50min_fri_night }}<br>
        <b>Tzeis 72 Minutes</b>{{ day.tzeis72min_fri_night }}<br>
        <hr>
      </div>
    </div>
    <!-- {{ calendar }} -->
  </div>
</template>

<style>
#grid-container {
  display: grid;
  /* grid-template-columns: 1fr 1fr 1fr; */
  gap: 10px;
  grid-auto-rows: minmax(100px, auto);
}

/* #grid-item {
  grid-column: 1 / 1;
} */
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Whole calendar",
      search: "",
      calendar: [],
    };
  },
  created: function () {},
  methods: {
    getWholeCalendar: function () {
      var params = {
        search: this.search,
      };
      axios.get(`/api/calendar?search=${this.search}`).then((response) => {
        console.log(response.data);
        this.calendar = response.data;
      });
    },
  },
};
</script>

