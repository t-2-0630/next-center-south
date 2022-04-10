<template>
  <div id="app">
    <ul v-for="tt in result" v-bind:key="tt.time+tt.line+tt.direction" class="list-group">
      <li class="list-group-item">
        <h4>{{ tt.line }}</h4>
        <h5>{{ tt.time |dateformat}}</h5>
        {{ tt.direction }} 方面行き<br />
      </li>
    </ul>
  </div>
</template>

<script>
import timetable from "./timetable";
export default {
  name: "App",
  data: function () {
    return {
      result: [],
    };
  },
  mounted: async function () {
    const tt = await timetable();
    const now = new Date();
    const index = tt.findIndex((item) => {
      return item.time > now;
    });
    this.result = tt.slice(index, index + 6);
    console.log(this.result)
  },
  filters:{
    dateformat:function(date){
      return `${String(date.getHours()).padStart(2,"0")}:${String(date.getMinutes()).padStart(2,"0")}`
    }
  }
};
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
