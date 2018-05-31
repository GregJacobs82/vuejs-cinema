<template>
	<div id="day-select">
		<ul class="days">
			<li
			class="day"
			v-for="day in days"
			v-on:click="selectDay(day)"
			:class="{ day: true, active: isActive(day) }">
				{{ formatDay(day) }}
			</li>
		</ul>
		<div class="clock">
			<div class="dateNow">
				<span>{{ monthNow }}</span>
				<span>{{ dayNow }}</span>
			</div>
			<span class="timeNow">{{ timeNow }}</span>
		</div>
	</div>
</template>
<script>
	export default {
		props: ['selected'],
		data() {
			return {
				days: [0, 1, 2, 3, 4, 5, 6].map(num => this.$moment().add(num, 'days'))
			}
		},
		methods: {
			formatDay(raw) {
				if (raw.isSame(this.$moment(), 'day')) {
					return 'Today';
				} else {
					return raw.format('ddd: MMM D');
				}
			},
			isActive(day) {
				return day.isSame(this.selected, 'day');
			},
			selectDay(day) {
				this.$bus.$emit('set-day', day);
			}
		},
		computed: {
		    timeNow() {
		        return this.$moment().format('h:mma');
			},
			monthNow() {
                return this.$moment().format('MMM');
			},
			dayNow() {
		        return this.$moment().format('D');
			},
		}
	}
</script>

<style lang="scss">
	#day-select {
		display:flex;
	}
	.clock {
		padding: 0px 15px;
		background: #161616;
		display: flex;
		align-items: center;
		color: #6e6e6e;
	}
	.dateNow {
		font-size:.65rem;
		text-align:center;
		color:#bbb;
		background:#3f3f3f;
		width: 35px;
		height:35px;
		display:flex;
		flex-direction:column;
		align-items:center;
		justify-content:center;
		margin-right:10px;
	}
</style>