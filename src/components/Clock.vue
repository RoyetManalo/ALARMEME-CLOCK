<template>
    <div id="clock">
        <CurrentTime :currentTime="currentTime"/>
        <Alarm :alarmValue="alarmValue"/>
        <div id="button">
            <div id="hourButton">
                <AlarmButton @clear="$emit('clear')" @btn-rapid-plus="$emit('btn-rapid-hour-plus')" @btn-rapid-minus="$emit('btn-rapid-hour-minus')" :isDisabled="isDisabled"/>
            </div>
            <div id="minuteButton">
                <AlarmButton  @clear="$emit('clear')"  @btn-rapid-plus="$emit('btn-rapid-minute-plus')" @btn-rapid-minus="$emit('btn-rapid-minute-minus')"  :isDisabled="isDisabled"/>
            </div>
        </div>
    </div>
      
</template>


<script>
    import CurrentTime from './CurrentTime.vue'
    import Alarm from './Alarm.vue'
    import AlarmButton from './AlarmButton.vue'
   
    export default {
        name: 'Clock',
        components: {
            CurrentTime,
            Alarm,
            AlarmButton,
        },
        props:{
            currentTime: Object,
            alarmValue: Object,
            isAlarming: Boolean,
            isDisabled: String
        },
        data(){
            return {
                interval: 0 //declaring the interval value as undefine
            }
        },
        methods:{
            formatNumber: num =>( num < 10 ? "0" + num : num) ,
            setAlarm(){
                if(this.isAlarming){
                    this.isAlarming = false
                    this.checkAlarmStatus()
                }else{
                    this.isAlarming = true
                    this.checkAlarmStatus()
                }
                console.log(this.isAlarming)
            },
            checkCurrentTime(){
                const currentTime = `${this.formatNumber(this.hourDisplay)}:${this.formatNumber(this.minuteDisplay)}`
                const alarmValue = `${this.formatNumber(this.alarmHour)}:${this.formatNumber(this.alarmMinute)}`
                console.log(currentTime)
                console.log(alarmValue)

                if(alarmValue === currentTime){
                    console.log('Wake Up')
                }
            },
            checkAlarmStatus(){
                if(this.isAlarming){
                this.interval = setInterval(this.checkCurrentTime, 1000)
                }else{
                    clearInterval(this.interval)
                }
            }
        },
        emits: ['clear', 'btn-rapid-hour-plus', 'btn-rapid-hour-minus', 'btn-rapid-minute-plus', 'btn-rapid-minute-minus']
    }
</script>


<style scoped>
    #clock {
        background: #2c2c2c;
        color: #fff;
        width: 360px;
        height: auto ;
        padding: 1.5rem 2rem;
        border-radius: 10px;
        margin-top: 2rem;
    }
    
    #button {
        display: flex;
        align-items: center;
        justify-content: space-around;
    }

</style>