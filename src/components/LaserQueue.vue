<template>
  <div id="app">
    <div class="container">
      <div class="card">
        <queue-header>
          <span>LASER CUTTER QUEUE</span>
        </queue-header>
        <cutter-header :onCutterRows="onCutter">
          <span>On Cutter</span>
        </cutter-header>
        <cutter-table
          :onCutterRows="onCutter"
          :timeOnRows="timeOn"
          :cutTimeRows="cutTimes"
          :timeRows="times"
        ></cutter-table>
        <sign-up-header>
          <span>Sign In</span>
        </sign-up-header>
        <sign-up-form :onQueueRows="onQueue" :timeInRows="timeIn"></sign-up-form>
        <on-queue-header>
          <span>On Queue</span>
        </on-queue-header>

        <!-- On-Queue Table -->
        <on-queue-table
          :onQueueRows="onQueue"
          :timeInRows="timeIn"
          :onCutterRows="onCutter"
          :timeOnRows="timeOn"
          :timeRows="times"
        ></on-queue-table>
      </div>
    </div>
  </div>
</template>

<script>
import QueueHeader from "./QueueHeader";
import CutterHeader from "./CutterHeader";
import CutterTable from "./CutterTable";
import SignUpHeader from "./SignUpHeader";
import SignUpForm from "./SignUpForm";
import OnQueueHeader from "./OnQueueHeader";
import OnQueueTable from "./OnQueueTable";

export default {
  name: "LaserQueue",
  components: {
    QueueHeader,
    CutterHeader,
    CutterTable,
    SignUpHeader,
    SignUpForm,
    OnQueueHeader,
    OnQueueTable,
  },
  props: {
    onQueue: Array,
    onCutter: Array,
    timeIn: Array,
    timeOn: Array,
    times: Array,
    cutTimes: Array,
    time: Number,
  },
};
</script>

<style>
.card {
  display: flex;
  align-self: center;
  margin-top: 5%;
}

.main-header {
  background-color: white;
  color: rgb(2, 196, 255);
}

.queue-header {
  color: rgb(7, 7, 75);
  background-color: rgb(255, 230, 0);
  margin-bottom: 0;
}

.queue-body {
  outline: solid rgb(2, 196, 255);
}
</style>