<template>
    <div class="currentTimeDiv">
        <p>Current Time</p>
        <span id="currentTime">{{this.formatNumber(currentTime.hourDisplay)}}:{{this.formatNumber(currentTime.minuteDisplay)}}:{{this.formatNumber(currentTime.secondsDisplay)}}</span>
    </div>
</template>


<script>
    export default {
        name: 'CurrentTime',
        props:{
            currentTime: Object
        },
        methods:{
            formatNumber: num =>( num < 10 ? "0" + num : num) 
        }
}

</script>


<style scoped>
    .currentTimeDiv {
    display: flex;
    justify-content: space-between;
    padding: 0 1.5rem;
    font-family: "Kiwi Maru", serif;
}
</style>