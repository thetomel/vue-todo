<script>
import axios from 'axios';
// import {ref} from 'vue';
export default {
    name: 'ToDoItem',
    props: {
    taskName: String,
    taskDesc: String,
    user: String,
    done: Boolean,
    uploadDate: Date,
    taskid: Number
  },
  data(){
    return {
    base_url: 'http://localhost:8080/tasks',
    doneLocal: this.done}
    
  },
  methods:
  {
      dateBuilder() {
      let d = new Date(this.uploadDate);
      console.log(d)
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()]
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      let hour = d.getHours();
      let minutes = d.getMinutes();

      return `${hour}:${minutes} - ${day} ${date} ${month} ${year}`
      }
,
changeDone(){
        this.doneLocal =!this.doneLocal
        let url_patch = ( '/' + this.taskid + '/state')
        console.log('link' + this.doneLocal)
        axios.patch(this.base_url + url_patch);
      }
}
  }

</script>
<template>
    <div class="todoitem">
        <div :class="doneLocal ? 'done' : 'def'">
        <section @click="changeDone()">
        
        <b>{{ taskName }}</b>  
        </section>
        <p class="description">{{ taskDesc}}</p>
        <p><b>Owner:</b> {{ user}}</p>
        {{dateBuilder()}}</div>
        
    </div>
    
</template>
<style scoped>
.todoitem {
    border: black 6px solid;
}
.todoitem section b {
    font-size: 30px;
}
.done{
    text-decoration: line-through;
    text-decoration-color: #001133;
    color: darkgray
}
.def{
    color: #001133
}
</style>