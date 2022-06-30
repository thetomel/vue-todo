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
            base_url: 'http://localhost:8080/tasks'
        };
    },
    mounted() {
        axios.get(this.base_url).then(response => (this.tasks = response.data)).catch(error => {console.log(error), this.errored=true})
        console.log(this.tasks);
    },
    // updated() {
    //     axios.get(this.base_url).then(response => (this.tasks = response.data)).catch(error => {console.log(error), this.errored=true})
    //     console.log(this.tasks);
    // },
    components: { ToDoItem, AddTaskVue },
  
}
</script>

<template>
<div v-if="errored">
<p> </p></div>
<div v-else>
  <div id="TasksListComponent">
    <add-task-vue></add-task-vue>
    <ul class="ListOfTasks">
        <li v-for="item in tasks" v-bind:key="item.lastUpdate">
            <ToDoItem :taskName="item.taskName" :taskDesc="item.taskDescription" :user="item.userName" :uploadDate="item.uploadDate" :done="item.done" :taskid="item.taskID"></ToDoItem>
        </li> 
    </ul>
  
    
</div> 
</div>
</template>