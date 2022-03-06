<template>
   <footer>
        <p>This is a simple project by Royet Manalo</p>
        <p>The goal of this project is to improve my VUE Javascript skills and knowledge</p>
        <p>Copyright &copy; 2021</p>
   </footer>
    
</template>


<script>
    export default {
        name: 'Footer',
        components: {
           
        }
    }
</script>


<style scoped>
    footer{
        font-family: "Kiwi Maru", serif;
        font-size: 12px;
        color: #fff;
        text-align: center;
        position: fixed;
        bottom: 0;
        left: 50%;
        transform: translate(-50%, -50%);
        line-height: 1.5;
        z-index: 5;
        
    }

    footer::before {
        content: "";
        position: absolute;
        background: black;
        border-radius: 10px;
        opacity: 0.5;
        z-index: -1;
        width: 500px;
        height: 70px;
        bottom: 0;
        left: 50%;
        transform: translate(-50%, 10%);
    } 
  
</style>