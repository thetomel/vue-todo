<script>
import axios from 'axios';
import ToDoItem from './ToDoItem.vue';

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
    },
    components: { ToDoItem },
  
}
</script>

<template>
<div v-if="errored">
<p> </p></div>
<div v-else>
  <div id="TasksList">
    <ul>
        <li v-for="item in tasks">
            <ToDoItem :taskName="item.taskName" :taskDesc="item.taskDescription" :user="item.userName" :uploadDate="item.uploadDate" :done="item.done"></ToDoItem>
        </li> 
    </ul>
  
    
</div> 
</div>
</template>