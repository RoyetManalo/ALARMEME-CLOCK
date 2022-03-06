<template>
  <h1 :class="isAlarmOn ? 'blinking' : 'notBlinking'">{{text}}</h1>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'Message',  
  props:{
    text: String,
    isAlarmOn: Boolean,
  },
}
</script>

<style scoped>
    h1{
        color:#fff;
        margin-top: 1rem;
        font-size: 5rem;
    }
    /* I used class based transition and animation */
    .blinking{
      animation: blinker 1s linear infinite
    }

    .notBlinking{
      animation: none;
    }

    @keyframes blinker {
      50% {
      opacity: 0;
    }
}

</style>
