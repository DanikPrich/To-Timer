<template>
<div>
  <section class="timer-section section">
    <div class="container">
      <input type="date" class="timer-section__input" v-model="deadline" :min="tomorrowDate">
      <my-timer :deadline="deadline"/>
    </div>
  </section>
</div>
</template>

<script>
import MyTimer from "../components/MyTimer.vue"
export default {
  name: 'HomeView',
  data() {
    return {
      deadline: '2022-10-22',
      tomorrowDate: ''
    }
  },
  components: {
    MyTimer
  },
  methods: {
    getTomorrowDate() {
      //Function for finds YYYY-MM-DD format tomorrow date
      let date = new Date();
      date.setDate(date.getDate() + 1);
      return new Date(date.getTime() - (date.getTimezoneOffset() * 60000 )).toISOString().split("T")[0];
      
    }
  },
  mounted() {
    this.tomorrowDate = this.getTomorrowDate()
    this.deadline = this.tomorrowDate
  }
}
</script>

<style lang="sass" scoped>
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@300;500&display=swap')

.timer-section
  font-family: 'Rubik', sans-serif
  &__input
    margin-bottom: 50px
    font-size: 30px
    background-color: rgb(255, 168, 37)
    border: 0
    font-family: 'Rubik', sans-serif
    font-weight: 300
    padding: 10px
    border-radius: 11px
    background: #ffa825
    box-shadow:  6px 6px 11px #db9020, -6px -6px 11px #ffc02a
    &:focus
      border: none
  

section
  padding: 300px 0

.container 
  max-width: 1000px
  margin: auto

@media (max-width: 1050px) 
  .container
    max-width: 800px
  .timer-section__input
    font-size: 25px
  section
    padding: 250px 0

@media (max-width: 830px) 
  .container
    max-width: 600px
  .timer-section__input
    font-size: 18px
    margin-bottom: 30px
  section
    padding: 200px 0

@media (max-width: 640px) 
  .container
    max-width: 500px
  .timer-section__input
    font-size: 14px
    margin-bottom: 20px
  section
    padding: 100px 0

@media (max-width: 530px) 
  .container
    max-width: 300px
  .timer-section__input
    font-size: 14px
    margin-bottom: 20px
  section
    padding: 100px 0
</style>