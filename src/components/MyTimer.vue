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
		width: 200px
		padding: 10px
		margin-right: 30px
		border-radius: 16px
		background: #ffa825
		box-shadow:  8px 8px 25px #de9220, -8px -8px 25px #ffbe2a
		&:last-child
			margin-right: 0
	
@media (max-width: 1050px) 
	.timer
		font-size: 60px
		&__text
			font-size: 40px
		&__item		
			width: 180px
			padding: 5px
			margin-right: 20px
			border-radius: 16px
			background: #ffa825
			box-shadow:  8px 8px 25px #de9220, -8px -8px 25px #ffbe2a
			&:last-child
				margin-right: 0


@media (max-width: 830px) 
	.timer
		font-size: 45px
		&__text
			font-size: 30px
		&__item		
			width: 135px
			padding: 5px
			margin-right: 20px
			border-radius: 16px
			background: #ffa825
			box-shadow:    7px 7px 14px #de9220, -7px -7px 14px #ffbe2a
			&:last-child
				margin-right: 0


@media (max-width: 640px) 
	.timer
		font-size: 30px
		&__text
			font-size: 20px
		&__item
			width: 135px
			padding: 5px
			margin-right: 20px
			border-radius: 16px
			background: #ffa825
			box-shadow:    7px 7px 14px #de9220, -7px -7px 14px #ffbe2a
			&:last-child
				margin-right: 0

@media (max-width: 530px) 
	.timer
		font-size: 20px
		&__text
			font-size: 12px
		&__item
			width: 50px
			padding: 5px
			margin-right: 20px
			border-radius: 8px
			background: #ffa825
			box-shadow: 5px 5px 10px #de9220, -5px -5px 10px #ffbe2a
			&:last-child
				margin-right: 0

	

</style>