<template>
  <div>
    <div class="row d-flex justify-content-center">
      <div class="timer">
        <span id="minutes">{{minutes >= 10 ? null : leadingZeroStr}}{{minutes}}:</span>

        <span id="seconds">{{seconds >= 10 ? null : leadingZeroStr}}{{seconds}}</span>
      </div>
    </div>
    <div class="row d-flex justify-content-center">
      <span id="milliseconds">.{{ !started ? zeroString : milliseconds}}</span>
    </div>
    <br />
    <div class="row d-flex justify-content-center">
      <button @click="start" class="btn btn-success">{{!started ? buttonStrStart : buttonStrResume}}</button>
      <button @click="pause" class="btn btn-primary">Pause</button>
      <button @click="resetTimer" class="btn btn-warning">Reset</button>
      <button @click="stop" class="btn btn-danger">Stop</button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    stop() {
      console.log("??");
    },
    resetTimer() {
      this.minutes = 0;
      this.seconds = 0;
      this.milliseconds = 0;
    },
    pause() {
      this.paused = true;
    },
    start() {
      if (this.paused) {
        this.paused = false;
      }
      this.started = true;
      console.log(this.started);
      this.startTimer();
    },
    startTimer() {
      let startTime = Date.now();

      let timer = setInterval(() => {
        if (this.paused) {
          clearInterval(timer);
        }

        let elaspsedTime = Date.now() - startTime;
        this.milliseconds = elaspsedTime;

        if (this.milliseconds >= 1000) {
          this.milliseconds = 0;
          this.seconds += 1;
          startTime = Date.now();
        }
        if (this.seconds === 60) {
          this.seconds = 0;
          this.minutes += 1;
        }
      });
    }
  },
  data() {
    return {
      minutes: 9,
      seconds: 55,
      milliseconds: 0,
      zeroString: "000",
      leadingZeroStr: "0",
      started: false,
      paused: false,
      reset: false,
      buttonStrStart: "Start",
      buttonStrResume: "Resume"
    };
  }
};
</script>

<style>
#minutes,
#seconds {
  font-size: 10em;
  font-family: "Orbitron", sans-serif;
}
#milliseconds {
  font-size: 5em;
  font-family: "Orbitron", sans-serif;
}
.btn {
  margin-right: 5px;
}
</style>