<template>
      <div id="modeToggle">
        <i @click="$emit('day-night-toggle')" :class="toggleClass" id="day"></i>
    </div>
</template>

<script>
// @ is an alias to /src


export default {
  name: 'Toggle',
  components: {
   
  },
  props:{
    toggleClass: String
  },
  emits: ['day-night-toggle']
}
</script>

<style scoped>
    #modeToggle {
        position: absolute;
        top: 15px;
        left: 15px;
        color: #fff;
        
    }
</style>
