<template>
  <div id="app">
    <!-- import bootstrap -->
    <link
      rel="stylesheet"
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.0/css/bootstrap.min.css"
      integrity="sha384-9gVQ4dYFwwWSjIDZnLEWnxCjeSWFphJiwGPXr1jddIhOegiu1FwO5qRGvFXOdJZ4"
      crossorigin="anonymous"
    />
    <!-- import Beam Queue script -->
    <LaserQueue
      :onQueue="onQueue"
      :onCutter="onCutter"
      :timeIn="timeIn"
      :times="times"
      :timeOn="timeOn"
      :cutTimes="cutTimes"
      :time="time"
      :firstName="firstName"
      :lastName="lastName"
    />
  </div>
</template>

<script>
import LaserQueue from "./components/LaserQueue.vue";

export default {
  name: "app",
  components: {
    LaserQueue
  },
  data() {
    return {
      onQueue: [],
      onCutter: [],
      timeIn: [],
      times: [],
      cutTimes: [],
      timeOn: [],
      time: 0,
      firstName: "",
      lastName: ""
    };
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>