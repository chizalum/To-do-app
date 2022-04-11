<template>
  <div id="shopping-list">
   <h1 id="head">Todo App</h1>

   <!-- Input -->
   <!-- v-model directive is used to create two way data communication on input-->
   <div>
    <input v-model="task" type="text" id="input" placeholder="Enter Task">
    <button id="btn" @click="submitTask">SUBMIT</button>
    <table>
    <caption>Taskbar </caption>
      <thead>
        <tr> 
        <th>Task</th>
        <th>Status</th>
        <th>Edit</th>
        <th>Delete</th>
      </tr>
      </thead>
      <!-- v-for used in linking to the data -->
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{task.name}}</td>
          <td><span @click="changeStatus(index)">{{task.status}}</span></td>
          <td>
            <div id="edit" class="change" @click="editTask(index)"><span class="text">&#9998;</span></div>
          </td>
         <td>
            <div id="delete" class="change" @click="deleteTask(index)"><span class="text">&#x1F5D1;</span></div>
          </td>
          </tr>
        </tbody>
    </table>
   </div>
  </div>
</template>

<!-- data function returns an objecct -->
<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return {
      task: '',
      editedTask: null,
      availableStatuses: ['To-do', 'In-progress', 'Finished'],

      tasks: [
        {
          name: 'wake up',
          status: 'To-do',
        },
        {
          name: 'Go jogging',
          status: 'In-progress',
        },
      ]
    }
  },

  methods: {
    submitTask(){
      if(this.task.length === 0) return;
      
      if(this.editedTask === null){
        this.tasks.push({
          name: this.task,
          status: 'To-do',
        });
        }else{
          this.tasks[this.editedTask].name =this.task;
          this.editedTask = null;
        }

      this.task ='';
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    
    changeStatus(index) {
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatuses[newIndex];
    },
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
<style>
  #input{
  width: 55vw;
  margin: auto;
  margin-left: 12%;
  }

  table, th, td {
  border: 1px solid black;
  width: 56vw;
  margin: auto;
  margin-left: 12%;
}

  #head{
  text-align: center;
  }

  .text{
  cursor: pointer; 
  width: 40px;
  }

  #delete{
  background: red;
  cursor: pointer;
  }

  #edit{
  background: rgb(207, 140, 14);
  cursor: pointer;
  }

  #btn{
  background:pink;
  }

  .change{
  text-align: center;
  }
</style>