<template>
    <div>
        <div class="timer">{{dateString}}</div>
        
        <div class="buttons">     
          <button class="start" v-on:click="start" v-show="!isStarted">Start</button>
          <button class="stop" v-on:click="stop" v-show="isStarted">Stop</button>

          <button class="pause" v-on:click="pause" v-show="!isStarted">Pause</button>
          <button class="rest" v-on:click="rest" v-show="!isStarted">Rest</button>
        </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "Timer",
  props: ["settings"],
  data: function() {
    return {
      timeStamp: null,
      isStarted: false,
      now: null
    };
  },
  methods: {
    start: function() {
      this.timeStamp = this.now.add(this.settings.timer, "minutes");
      this.isStarted = true;
    },
    stop: function() {
      this.timeStamp = null;
      this.isStarted = false;
    },
    getDateTime() {
      this.now = moment();
    },
    pause: function() {
      this.timeStamp = this.now.add(this.settings.pause, "minutes");
      this.isStarted = true;
    },
    rest: function() {
      this.timeStamp = this.now.add(this.settings.rest, "minutes");
      this.isStarted = true;
    }
  },
  created() {
    setInterval(this.getDateTime, 1000);
  },
  destroyed() {
    clearInterval(this.getDateTime);
  },
  computed: {
    dateString: function() {
      let diff = 0;
      if (this.timeStamp) {
        diff = this.timeStamp.diff(this.now);
        if (diff < 0) {
          this.stop();

          return "Great job!";
        }
      }

      return moment(diff).format("mm:ss");
    }
  }
};
</script>

<style>
.timer {
  font-size: xx-large;
  color: #42b983;
  margin: 10px;
}

.buttons button {
  font-size: large;
  margin: 5px;
}

button.start {
  color: green;
}
button.stop {
  color: red;
}
button.pause {
  color: blueviolet;
}
button.rest {
  color: violet;
}
</style>


