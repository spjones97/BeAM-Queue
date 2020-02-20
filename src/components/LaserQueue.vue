<template>
  <div id="app">
    <div class="container">
      <div class="card">
        <!-- Main Card header -->
        <h1 class="card-header main-header">LASER CUTTER QUEUE</h1>

        <!-- Cutter Header -->
        <h3 v-cloak v-if="onCutter.length > 0" class="cutter-header">
          On
          Cutter
        </h3>

        <!-- On-Cutter Table -->
        <table v-cloak v-if="onCutter.length > 0" class="table">
          <thead class="thead-light">
            <th>#</th>
            <th>Name</th>
            <th>Start Time</th>
            <th>Expected End Time</th>
            <th>Remove</th>
          </thead>
          <tbody class="cutter-body">
            <tr v-cloak v-for="(p, index) in onCutter" :key="index">
              <td>{{ index + 1 }}</td>
              <td>{{ getCutterName(index) }}</td>
              <td>{{ currentTime }}</td>
              <td id="timer">{{ getTime(index) }}</td>
              <td>
                <button type="button" @click="removeCutter(index)" class="btn btn-warning">REMOVE</button>
              </td>
            </tr>
          </tbody>
        </table>

        <!-- Sign-Up Form Header -->
        <h2 class="sign-header">Sign In</h2>

        <!-- Sign-Up Form -->
        <div class="signcontainer">
          <form v-cloak class="m-3">
            <div class="form-row">
              <div class="col">
                <input class="firstin" type="text" v-model="firstName" placeholder="First Name" />
              </div>
              <div class="col">
                <input class="lastin" type="text" v-model="lastName" placeholder="Last Name" />
              </div>
              <div class="col">
                <button
                  class="btn"
                  type="button"
                  @click="addToQueue(firstName, lastName)"
                  id="queuebtn"
                >ADD</button>
              </div>
            </div>
          </form>
        </div>

        <!-- Queue header -->
        <h3 class="queue-header">On Queue</h3>

        <!-- On-Queue Table -->
        <table class="table">
          <thead class="thead-light">
            <th>#</th>
            <th>Name</th>
            <th>Time-In</th>
            <th>Checks</th>
            <th>Time</th>
            <th>Add to Cutter</th>
          </thead>
          <tbody>
            <tr v-cloak v-for="(p, index) in onQueue" :key="index">
              <td>{{ index + 1 }}</td>
              <td>{{ getQueueName(index) }}</td>
              <td>{{ getTimeIn(index) }}</td>
              <td>
                <input type="checkbox" id="checkOne" />
                <label for="checkOne">#1</label>
                <input type="checkbox" id="checkTwo" />
                <label for="checkTwo">#2</label>
                <input type="checkbox" id="checkThree" />
                <label for="checkThree">#3</label>
              </td>
              <td>
                <input type="text" max="90" id="minInput" v-model="time" placeholder="min" />
              </td>
              <td>
                <button type="button" @click="addToCutter(index, time)" class="btn">ADD</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LaserQueue",
  props: {
    onQueue: Array,
    onCutter: Array,
    timeIn: Array,
    times: Array,
    cutTimes: Array,
    time: Number,
    firstName: String,
    lastName: String
  },
  computed: {
    // Returns number of people on the Queue
    numQueue: function() {
      return this.onQueue.length;
    },
    // Returns number of people on the Laser Cutter
    numCutter: function() {
      return this.onCutter.length;
    },
    // Returns the current time
    currentTime: function() {
      var today = new Date();
      return today.toLocaleTimeString();
    }
  },
  methods: {
    // Add person to the Queue
    addToQueue: function(first, last) {
      var name = first + " " + last;
      this.onQueue[this.onQueue.length] = name;
      var today = new Date();
      this.timeIn[this.timeIn.length] = today.toLocaleTimeString();
      this.onQueue.splice();
      this.timeIn.splice();
    },
    // Add person from the Queue to the Laser Cutter
    addToCutter: function(index, time) {
      this.onCutter[this.onCutter.length] = this.onQueue[index];
      var now = new Date();
      now.setMinutes(now.getMinutes() + parseInt(time));
      this.times[this.times.length] = now.toLocaleTimeString();
      this.onQueue.splice(index, 1);
      this.onCutter.splice();
    },
    // Removes person from the Laser Cutter
    removeCutter: function(index) {
      this.onCutter.splice(index, 1);
      this.cutTimes.splice(index, 1);
    },
    // Returns Name of person in the Queue
    getQueueName: function(index) {
      return this.onQueue[index];
    },
    // Returns Name of person on the Cutter
    getCutterName: function(index) {
      return this.onCutter[index];
    },
    // Returns Time person checked in
    getTimeIn: function(index) {
      return this.timeIn[index];
    },
    // Returns amount of Time cut is going to take
    getTime: function(index) {
      return this.times[index];
    }
  }
};
</script>

<style>
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

.card {
  display: flex;
  align-self: center;
  margin-top: 5%;
}

.main-header {
  background-color: white;
  color: rgb(7, 7, 75);
}

.cutter-header {
  background-color: red;
  color: white;
}

.queue-header {
  color: rgb(7, 7, 75);
  background-color: rgb(255, 230, 0);
}

.cutter-body {
  outline: solid red;
}
</style>