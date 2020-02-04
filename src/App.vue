<template>
  <div id="app">
    <!-- import bootstrap -->
    <link
      rel="stylesheet"
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.0/css/bootstrap.min.css"
      integrity="sha384-9gVQ4dYFwwWSjIDZnLEWnxCjeSWFphJiwGPXr1jddIhOegiu1FwO5qRGvFXOdJZ4"
      crossorigin="anonymous"
    />
    <LaserQueue
      :onQueue="onQueue"
      :onCutter="onCutter"
      :timeIn="timeIn"
      :times="times"
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
.signcontainer {
  display: flex;
  justify-content: space-around;
}

.firstin {
  width: 25vw;
}

.lastin {
  width: 25vw;
}

.oncutter-header,
.onqueue-header,
.signup-header {
  text-align: center;
  text-decoration: underline;
}
</style>