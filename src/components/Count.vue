<template>
   <div>
     {{num}}
     <button @click="increment">increment</button>
     <button @click="decrement">decrement</button>
     <button @click="reset">reset</button>
   </div>
</template>


<script>
    export default{
        name:"Count",
        data() {
            return {
                num: 0,
            }
        },
        methods:{
            increment(){
               this.num++;
            },
            decrement(){
               if(this.num > 0)this.num--;
            },
            reset(){
                this.num = 0;
            }
        }
    }
</script>


<style>
</style>