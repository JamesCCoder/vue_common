<template>
    <div>
        <input v-model="newTask"/>
        <button @click="addClick">add</button>
        <div v-for="(task, index) in tasks" :key="index">
            <div v-if="!task.editable">{{task.name}}</div>
            <input v-else v-model="task.name"/>
            <button @click="editClick(index)">edit</button>
            <button @click="deleteClick(index)">delete</button>
        </div>
    </div>
</template>

<script>
    export default {
        name:"Test",
        data(){
            return{
                newTask:"",
                tasks:[
                    {
                        name:"task1", editable:false,
                    },
                    {
                        name:"task2", editable:false,
                    }
                ]
            }
        },
        methods:{
           addClick(){
               if(this.newTask.trim() !== ""){
                   this.tasks.push({
                      name:this.newTask,
                      editable:false,
                   })
               };
               this.newTask=""
           },
           editClick(index){
               this.tasks[index].editable = !this.tasks[index].editable;
           },
           deleteClick(index){
               this.tasks.splice(index, 1);
           }
        }
    }
</script>

<style scoped>

</style>