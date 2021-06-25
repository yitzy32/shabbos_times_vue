<template>
  <div class="calendar">
    <h1>{{ message }}</h1>
    <input type="text" v-model="search">
    <button v-on:click="getWholeCalendar()">Search</button>
    {{ calendar }}
  </div>
</template>

<style>
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

