<template>
  <Toggle @day-night-toggle="$emit('day-night-toggle')" :toggleClass="day ? 'fas fa-sun fa-3x' : 'fas fa-moon fa-3x'" />
  <Clock :currentTime="currentTime" :alarmValue="alarmValue" :isDisabled="isDisabled" @clear="clearTimers" @btn-rapid-hour-plus="rapidPlusHour" @btn-rapid-hour-minus="rapidMinusHour" @btn-rapid-minute-plus="rapidPlusMinute" @btn-rapid-minute-minus="rapidMinusMinute"/>
  <Message v-show="isAlarming" :isAlarmOn="isAlarmOn" :text="isAlarmOn ? 'Wake Up' : 'Alarm is set'"/>
  <div class="btn">
    <Button :isAlarming="isAlarming" :text="isAlarming ? 'Cancel Alarm' : 'Set Alarm'" :className="isAlarming ? 'cancelAlarm' : 'setAlarm'"  @set-alarm="setAlarm"/>
    <Button v-show="isAlarmOn" text="Snooze" @click="snoozeAlarm"/> 
  </div>
   <Right v-show="isAlarmOn"/>
   <Left v-show="isAlarmOn"/>
   <Bottom v-show="isAlarmOn"/>

</template>

<script>
// @ is an alias to /src

import Clock from '../components/Clock.vue'
import Toggle from '../components/Toggle.vue'
import Message from '../components/Message.vue'
import Button from '../components/Button.vue'
import Left from '../components/Left.vue'
import Right from '../components/Right.vue'
import Bottom from '../components/Bottom.vue'
export default {
  name: 'Home',
  components: {
    Clock,
    Toggle,
    Message,
    Button,
    Left,
    Right,
    Bottom,
  },
  props:{
    day: Boolean
  },
  data(){
    return{
      // change the display into an object and the alarmvalue
      alarmValue:{
        alarmHour: 0,
        alarmMinute: 0,
      },
      currentTime:{
        hourDisplay: 0,
        minuteDisplay: 0,
        secondsDisplay: 0,
      },
      interval: 0, //declaring the interval value as undefine
      btnInterval :0,
      btnTimeout: 0,
      isAlarming: false,
      isAlarmOn: false,
      isDisabled: 'auto', //this is a pointerEvents
      audio: "" //declaring the audio value as undefine then declare the value in the mounted lifecycle hooks

    }
  },
  methods:{
    formatNumber: num =>( num < 10 ? "0" + num : num) ,
    startTime(){ 
      const timer = setInterval(() =>{
        let date = new Date()
        let hour = date.getHours()
        let minute = date.getMinutes()
        let seconds = date.getSeconds()

        this.currentTime.hourDisplay = hour
        this.currentTime.minuteDisplay = minute
        this.currentTime.secondsDisplay = seconds
      }, 1000)     
    },
    setAlarm(){
      if(this.isAlarming){
        this.isAlarming = false
        this.isAlarmOn =  false 
        this.disableAlarmButtons()
        this.playAudio()
        this.checkAlarmStatus()
        if(this.day){
          return
        }else{
         this.$emit('set-alarm')
        }
      }else{
        this.isAlarming = true 
        this.disableAlarmButtons()
        this.playAudio()
        this.$emit('set-alarm')
        this.checkAlarmStatus()
        if(this.day){
          return
        }else{
         this.$emit('set-alarm')
        }
      }
    },
    checkCurrentTime(){
      const currentTime = `${this.formatNumber(this.currentTime.hourDisplay)}:${this.formatNumber(this.currentTime.minuteDisplay)}`
      const alarmValue = `${this.formatNumber(this.alarmValue.alarmHour)}:${this.formatNumber(this.alarmValue.alarmMinute)}`
      console.log(currentTime)
      console.log(alarmValue)

      if(alarmValue === currentTime){
          console.log('Wake Up')
          this.isAlarmOn = true
          this.playAudio()
          this.$emit('alarm')
          }
     },
     clearTimers(){
      clearTimeout(this.btnTimeout)
      clearInterval(this.btnInterval)
    },
    rapidPlusHour(){
      this.incrementHourValue()
      this.btnTimeout = setTimeout(() =>{
        this.btnInterval = setInterval(() =>{
         this.incrementHourValue()
        },50)
      },300)
    },
    rapidMinusHour(){
      this.decrementHourValue()
      this.btnTimeout = setTimeout(() =>{
        this.btnInterval = setInterval(() =>{
         this.decrementHourValue()
        },50)
      },300)
    },
    rapidPlusMinute(){
      this.incrementMinuteValue()
      this.btnTimeout = setTimeout(() =>{
        this.btnInterval = setInterval(() =>{
         this.incrementMinuteValue()
        },50)
      },300)
    },
    rapidMinusMinute(){
      this.decrementMinuteValue()
      this.btnTimeout = setTimeout(() =>{
        this.btnInterval = setInterval(() =>{
         this.decrementMinuteValue()
        },50)
      },300)
    },
    incrementHourValue(){
      this.alarmValue.alarmHour++
      if(this.alarmValue.alarmHour === 24){
        this.alarmValue.alarmHour = 0
      }
    },
    decrementHourValue(){
       this.alarmValue.alarmHour--
      if(this.alarmValue.alarmHour === -1){
        this.alarmValue.alarmHour = 23
        }
    },
    incrementMinuteValue(){
      this.alarmValue.alarmMinute++
      if(this.alarmValue.alarmMinute === 60){
        this.alarmValue.alarmMinute = 0
      }
    },
    decrementMinuteValue(){
      this.alarmValue.alarmMinute--
      if(this.alarmValue.alarmMinute === -1){
          this.alarmValue.alarmMinute = 59
      }
    },
    checkAlarmStatus(){
      if(this.isAlarming){
        this.interval = setInterval(this.checkCurrentTime, 1000)
      }else{
        clearInterval(this.interval)
      }
    },
    snoozeAlarm(){
      this.alarmValue.alarmMinute += 10
      if(this.alarmValue.alarmMinute >= 60){
        this.alarmValue.alarmMinute -= 60
        this.alarmValue.alarmHour += 1
      }
      this.isAlarming = true 
      this.isAlarmOn = false
      this.disableAlarmButtons()
      this.playAudio()
      this.$emit('set-alarm')
    },
    playAudio(){
      if(this.isAlarmOn){
        this.audio.play()
      }else{
        this.audio.pause()
        this.audio.currentTime = 0
     }
    },
    disableAlarmButtons(){
      if(this.isAlarming){
        this.isDisabled = 'none'
      }else{
        this.isDisabled = 'auto'
      }
    },
    

  },
  emits: ['day-night-toggle', 'set-alarm', 'alarm'],
  mounted(){
    this.startTime()
    this.audio = new Audio (require('../assets/C.mp3'))
    // the audio is not pausing - done / disable the buttons on alarm - done / the displayHours make it an object - done / rapid increasing value of the alarm / snooze bug 
  }
}
</script>

<style scoped>
  .btn{
    display: flex;
    gap: 1rem;
  }
  .clock{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    
  }
</style>