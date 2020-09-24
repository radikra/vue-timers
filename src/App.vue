<template>
  <div id="app">
	  <div class="content" id="timers">
		  <Timer v-for="(timer, index) in timers" :key="index" />
		  <button id="addBtn" class="add-timer" @click="addTimer">+</button>
	  </div>
  </div>
</template>

<script>
import Timer from './components/Timer.vue'

export default {
  name: 'App',
  components: {
    Timer
  },
  data() {
	  return {
		  timers: [1]
	  }
  },
  methods: {
	  addTimer() {
		  this.timers.push(this.timers.length + 1)
	  }
  }
}
</script>
