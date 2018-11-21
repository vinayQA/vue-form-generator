<template lang="pug">
	.input-group.date
<<<<<<< HEAD
		input.form-control(type="text", v-model="value", v-on:click="startTimer"
=======
		input.form-control(type="text", v-model="value", onclick="startTimer"
>>>>>>> 9fc6716728de29339bbfba6c5a689a6d0830cbcc
		:required="schema.required",
		:autocomplete="schema.autocomplete",
		:disabled="disabled",
		:placeholder="schema.placeholder",
		:readonly="schema.readonly",
		:name="schema.inputName",
		:id="getFieldID(schema)")
		span.input-group-addon
</template>

<script>
	 	import abstractField from "../abstractField";
	 	import { defaults } from "lodash";


   export default({
  name: "Timer",
  data(){
    return {
      times: [],
      animateFrame: 0,
      nowTime: 0,
      diffTime: 0,
      startTime: 0,
      isRunning: false
    };
  },
  methods: {
    setSubtractStartTime: function (event) {
      let time = typeof time !== 'undefined' ? time : 0;
      this.startTime = Math.floor(performance.now() - time);
    },
    startTimer: function (event) {
      let vm = this;
      vm.setSubtractStartTime(vm.diffTime);
      (function loop(){
        vm.nowTime = Math.floor(performance.now());
        vm.diffTime = vm.nowTime - vm.startTime;
        vm.animateFrame = requestAnimationFrame(loop);
      }());
      vm.isRunning = true;
    },
    stopTimer: function (event) {
      this.isRunning = false;
      cancelAnimationFrame(this.animateFrame);
    },
    pushTime: function (event) {
      this.times.push({
        hours: this.hours,
        minutes: this.minutes,
        seconds: this.seconds,
        milliSeconds: this.milliSeconds
				});
    },
    // clearAll: function () {
    //   this.startTime = 0;
    //   this.nowTime = 0;
    //   this.diffTime = 0;
    //   this.times = [];
    //   this.stopTimer();
    //   this.animateFrame = 0;
    // }
  },
  computed: {
    hours: function () {
      return Math.floor(this.diffTime / 1000 / 60 / 60);
    },
    minutes: function () {
      return Math.floor(this.diffTime / 1000 / 60) % 60;
    },
    seconds: function () {
      return Math.floor(this.diffTime / 1000) % 60;
    },
    milliSeconds: function () {
      return Math.floor(this.diffTime % 1000);
    }
  },
  filters: {
    zeroPad: function(value){
      let num = typeof num !== 'undefined' ? num : 2;
      return value.toString().padStart(num,"0");
    }
  }
});
</script>
