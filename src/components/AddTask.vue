<script>
import axios from 'axios';

// import axios from 'axios'
export default {
    name: 'AddTask',
    data(){
        return{
            base_url:'http://localhost:8080/tasks/new',
            taskName: '',
            taskDescription: ''
        }
        
    },
    methods:
    {
        addTask(){
            if(this.taskName == '') {
                alert("cant be null")//change to some notification with collors on site
            }
            else{
            axios.post('http://localhost:8080/tasks/new',{
                "taskName": this.taskName,
                "userName": "curr",
                "taskDescription": this.taskDescription
            })
            this.taskName = '';
            this.taskDescription = '';
            }
        }
    }
}

</script>
<template>
    <div class="addTaskBar">
        <input type='text' placeholder="Type here task name..." v-model="taskName" />
        <textarea v-model="taskDescription" placeholder="About this task..."/>
        <button @click="addTask()">Add Task</button>
    </div>

</template>
<style>
    .addTaskBar {
        padding: 2%;
        display: flex;
    }
    .addTaskBar *{
        margin: 2%;
    }
</style>
