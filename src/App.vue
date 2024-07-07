<template>
   <!-- <Count /> -->
   <!-- <TodoList /> -->
   <!-- <Calculator /> -->
   <!-- <CountdownTimer /> -->
   <!-- <Register /> -->
   <!-- <TicTacToe /> -->
    <Test />
</template>


<script>
 import TodoList from "./components/TodoList.vue";
 import Calculator from "./components/Calculator.vue";
 import CountdownTimer from "./components/CountdownTimer.vue";
 import Count from "./components/Count.vue";
 import Register from "./components/Register.vue";
 import TicTacToe from "./components/TicTacToe.vue";
 import Test from "./components/Test.vue";

 export default{
     name:"App",
     components:{
        //  Count,
        //  TodoList,
        //  Calculator,
        //  CountdownTimer,
        //  Register,
        //  TicTacToe,
        //  ParenttoChild,
        // TestParent,
        Test,
     }
 }
</script>


<style></style>
