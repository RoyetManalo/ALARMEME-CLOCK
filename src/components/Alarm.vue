<template>
    <div id="alarmDiv">
       <div>{{this.formatNumber(alarmValue.alarmHour)}}</div>
       <div>:</div>
       <div>{{this.formatNumber(alarmValue.alarmMinute)}}</div>
    </div>
</template>


<script>
    export default {
        name: 'Alarm',
        props:{
            alarmValue: Object
        },
        methods:{
            formatNumber: num =>( num < 10 ? "0" + num : num) ,
        },
    }
</script>


<style scoped>
    #alarmDiv {
        background: #181818;
        width: 100%;
        font-size: 5rem;
        display: flex;
        align-self: center;
        justify-content: center;
        text-align: center;
        color: #e73a52;
        font-family: "Orbitron";
        margin: 1rem 0;
        border-radius: 10px;
        /* padding: 0 1rem; */
    }
</style>