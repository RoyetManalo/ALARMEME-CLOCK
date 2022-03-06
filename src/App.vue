<template>
  <div class="div" :style="day ? morning : night"> 
     <div class="container" >
      <Header/>
      <router-view @day-night-toggle="dayNightToggle" @set-alarm="alarming" @alarm="alarm" :day="day"></router-view>
      <Footer/>
    </div> 
  </div>
</template>

<script>
  import Header from './components/Header'
  import Footer from './components/Footer'
  export default {
    components:{
      Header,
      Footer
    },
    data(){
      return{
        day: true,
        morning: {
          background: `url(${require('@/assets/morning.jpg')}) center center no-repeat`
        },
        night: {
          background: `url(${require('@/assets/nights.jpg')}) center bottom no-repeat`
        }
      }
    },
    methods:{
      dayNightToggle(){
        this.day = !this.day
      },
      alarming(){
        this.day = !this.day
      },
      alarm(){
        this.day = true
      }
    }
  }
</script>

<style >
  #app{
    height: 100vh;
    width: 100vw;
  }
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    user-select: none;
  }
  .div{
    height: 100vh;
    width: 100vw;
    /* transition: 1s ease-in; */
  }
  .container {
  max-width: 1100px;
  margin: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  }

</style>
