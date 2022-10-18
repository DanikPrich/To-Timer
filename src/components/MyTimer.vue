<template>
	<div class="timer">
		<div class="timer__item">
			<div class="timer__val">{{ days }}</div>
			<div class="timer__text">Days</div>
		</div>
		<div class="timer__item">
			<div class="timer__val">{{ hours }}</div>
			<div class="timer__text">Hours</div>
		</div>
		<div class="timer__item">
			<div class="timer__val">{{ minutes }}</div>
			<div class="timer__text">Minutes</div>
		</div>
		<div class="timer__item">
			<div class="timer__val">{{ seconds }}</div>
			<div class="timer__text">Seconds</div>
		</div>
		<!-- {{ days }} - {{ hours }} : {{ minutes }} : {{ seconds }} -->
	</div>
</template>

<script>
	export default {
		data() {
			return {
				days: 0,
				hours: 0,
				minutes: 0,
				seconds: 0,
				timeInterval: null
			}
		},
		props: {
			deadline: String
		},

		watch: {
			deadline() {
				this.timeInterval = setInterval(this.updateTimeValues, 1000);
      	this.updateTimeValues();   
			}
		},
		
		methods: {
			getTimeRemaining() {
        const t = Date.parse(this.deadline) - Date.parse(new Date()),
              days = Math.floor(t / (1000 * 60 * 60 * 24)),
              hours = Math.floor((t / (1000 * 60 * 60) % 24)),
              minutes = Math.floor((t / 1000 / 60 ) % 60),
              seconds = Math.floor((t / 1000 ) % 60);

        return {
            'total': t,
            'days': days,
            'hours': hours,
            'minutes': minutes,
            'seconds': seconds
        };
    	},

			getZero(num){
        if(num >=0 && num < 10){
            return `0${num}`;
        } else {
            return num;
        }
   	 	},

			updateTimeValues() {
				const t = this.getTimeRemaining();

				this.days = this.getZero(t.days);
				this.hours = this.getZero(t.hours);
				this.minutes = this.getZero(t.minutes);
				this.seconds = this.getZero(t.seconds);

				if (t.total <= 0) {
						clearInterval(this.timeInterval);
				}
			},

		},

		mounted() {
			this.timeInterval = setInterval(this.updateTimeValues, 1000);
      this.updateTimeValues();   
		}
			
	}
</script>

<style lang="sass" scoped>

.timer
	font-size: 90px
	display: flex
	justify-content: space-around
	&__text
		font-weight: 300
		font-size: 50px
	&__item
		margin-right: 40px
	&__item:last-child
		margin-right: 0
	
@media (max-width: 870px) 
	.timer
		font-size: 60px
		&__text
			font-size: 40px
		&__item
			margin-right: 20px
		&__item:last-child
			margin-right: 0

@media (max-width: 670px) 
	.timer
		font-size: 45px
		&__text
			font-size: 30px
		&__item
			margin-right: 20px
		&__item:last-child
			margin-right: 0

@media (max-width: 500px) 
	.timer
		font-size: 30px
		&__text
			font-size: 20px
		&__item
			margin-right: 10px
		&__item:last-child
			margin-right: 0
	

</style>