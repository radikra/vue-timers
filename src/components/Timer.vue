<template>
	<div class="timer" :class="{timer_on : isCounting, timer_off : !isCounting}">
		<div class="timer__data">
			<span v-if="countHours">{{ countHours }}:</span>
			<span v-if="countMinutes || countHours">{{ countMinutes }}:</span>
			<span>{{ countSeconds }}</span>
		</div>
		<div class="timer__control">
			<button class="timer__btn" v-if="!isCounting" @click="startCount">
				<svg class="ctrl-btn">
					<use xlink:href="@/assets/icons.svg#play"></use>
				</svg>
			</button>
			<button class="timer__btn" v-else @click="pauseCount">
				<svg class="ctrl-btn">
					<use xlink:href="@/assets/icons.svg#pause"></use>
				</svg>
			</button>
			<button class="timer__btn" @click="resetCount">
				<svg class="ctrl-btn">
					<use xlink:href="@/assets/icons.svg#stop"></use>
				</svg>
			</button>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Timer',
	data() {
		return {
			countSeconds: 0,
			countMinutes: 0,
			countHours: 0,
			isCounting: false,
			timerId: null
		}
	},
	methods: {
		startCount() {
			this.timerId = setInterval(() => {
				this.countSeconds++
				if (this.countSeconds > 59) {
					this.countMinutes++
					this.countSeconds = 0
				}
				if (this.countMinutes > 59) {
					this.countHours++
					this.countMinutes = 0
				}
			}, 1000)
			this.isCounting = true
		},
		pauseCount() {
			clearInterval(this.timerId)
			this.isCounting = false
		},
		resetCount() {
			clearInterval(this.timerId)
			this.countSeconds = 0
			this.countMinutes = 0
			this.countHours = 0
			this.isCounting = false
		}
	}
}
</script>