<template>
  <div class="calendar">
    <h1>{{ message }}</h1>
    <input type="text" v-model="search">
    <button v-on:click="getWholeCalendar()">Search</button>
    <div style="width: 90%">
      <vue-table-dynamic :params="params"></vue-table-dynamic>
    </div>
  </div>
</template>

<style>
</style>

<script>
import VueTableDynamic from "vue-table-dynamic";
import axios from "axios";

export default {
  name: "Demo",
  data() {
    return {
      message: "Whole Calendar",
      search: "",
      params: {
        data: [["Date", "Mincha Gedola", "Mincha", "Plag", "Candle Lighting", "Shkia", "Tzeis 50 Minutes"]],
        header: "row",
        border: true,
        stripe: true,
        highlight: { column: [-3] },
        highlightedColor: "rgb(255, 254, 209)",
      },
    };
  },
  components: { VueTableDynamic },
  methods: {
    getWholeCalendar: function () {
      var params = {
        search: this.search,
      };
      axios.get(`/api/calendar?search=${this.search}`).then((response) => {
        console.log(response.data);
        response.data.forEach((day) => {
          let nextRow = [];
          nextRow.push(
            day.date,
            day.mincha_gedola,
            day.mincha,
            day.plag_hamincha,
            day.candle_lighting,
            day.sunset,
            day.tzeis50min_fri_night
          );
          this.params.data.push(nextRow);
        });
        console.log(this.params.data);
      });
    },
  },
};
</script>

// library available from this site: https://vuejsexamples.com/a-vue-component-of-dynamic-table/