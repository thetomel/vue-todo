<script>
import axios from 'axios';
import ToDoItem from './ToDoItem.vue';
import AddTaskVue from './AddTask.vue';

export default {
    name: "TasksList",
    data() {
        return {
            query: "",
            tasks: {},
            errored: false,
            base_url: 'http://localhost:8080/tasks',
        };
    },
    mounted() {
        axios.get(this.base_url).then(response => (this.tasks = response.data)).catch(error => {console.log(error), this.errored=true})
        console.log(this.tasks);
    },
    methods:{
        reload(){
            this.$nextTick(()=>{
                axios.get(this.base_url).then(response => (this.tasks = response.data)).catch(error => {console.log(error), this.errored=true})
            });
        },
    },
        

    components: { ToDoItem, AddTaskVue },
    computed:
    {

    }
  
}
</script>

<template>
<div class="content" v-if="errored">
    <p>Error - can't get to Data</p>
</div>
<div class="content" v-else>
  <div id="TasksListComponent">
    <add-task-vue v-on:task-added="reload"></add-task-vue>
    <ul class="ListOfTasks">
        <li v-for="item in tasks" v-bind:key="item.uploadDate">
            <ToDoItem :taskName="item.taskName" :taskDesc="item.taskDescription" :user="item.userName" :uploadDate="item.uploadDate" :done="item.done" :taskid="item.taskID"></ToDoItem>
        </li> 
    </ul>
  
    
</div> 
</div>
</template>