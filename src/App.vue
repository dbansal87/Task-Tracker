<template>
<div class="container">
<Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
<AddTask v-show="showAddTask" @add-new-task="addTask"/>
<Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
</div>
</template>
x
<script>
import Header from './components/Header.vue'
import Tasks from './components/TasksList.vue' 
import AddTask from './components/AddTask.vue'
export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
},
data() {
  return {
    tasks: [],
    showAddTask: false
  }
},
methods: {
  async fetchTasks() {
    const res = await fetch("http://localhost:5000/tasks");
    const data = await res.json();
    return data;
  },
  async fetchTaskById(id) {
    const res = await fetch(`http://localhost:5000/tasks/${id}`);
    const data = await res.json();
    return data;
  },
  async addTask(newTask) {
  const res = await fetch("http://localhost:5000/tasks",{
  method: 'POST',
  headers: {'Content-Type': 'application/json'},
  body: JSON.stringify(newTask)
  });
  const data = await res.json();
    this.tasks = [...this.tasks, data]
  },
  toggleReminder(id) {
    const taskToToggle = await this.fetchTaskById(id);
    this.tasks = this.tasks.map(task => 
    task.id === taskToBeToggled.id ? {...task, reminder: !taskToBeToggled.reminder }: task
    )
  },
  async deleteTask(id) {
    if(confirm("Are you sure you wanna delete the task?")) {
      const res = await fetch(`http://localhost:5000/tasks/${id}`,{
      method:'DELETE'
    })
    res.status === 200 ? (this.tasks = this.tasks.filter(task => task.id !== id)) : 
    alert("Error while deleting the task")
    }
  },
  toggleAddTask(){
    this.showAddTask = !this.showAddTask
  }
},
async created() {
  this.tasks = await this.fetchTasks();
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
