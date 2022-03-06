<template>
   <button :class="className" @click="$emit('set-alarm')" id="setAlarm">{{text}}</button>
</template>

<script>
// @ is an alias to /src


export default {
  name: 'Button',
  props: {
    text: String,
    className: String
  },
  emits : ['set-alarm']
}
</script>

<style scoped>
    #setAlarm {
        background: rgb(235, 58, 58);
        color: #fff;
        font-size: 1.5rem;
        padding: 1rem 2rem;
        border-radius: 10px;
        margin-top: 2rem;
        width: 250px;
        text-align: center;
        border: none;
        /* animation-name: bodyopen;
        animation-duration: 1s; */
    }

</style>
