<template>
  <div>
    <div class="flex flex-center">
      <h1>{{ msg }}</h1>
    </div> 

    <div class="main">

      <form class="flex space-between" v-on:submit.prevent="addTask">
        <input class="add-task" type="text" placeholder="Ajouter une tâche" v-model="newTask" >
        <button type="submit">ADD</button>
      </form>
      
      <ul id="exemple">
        <div class="flex" v-for="task in tasks" :key="task.id">
          <li v-bind:class="[task.completed ? 'complete' : '']">{{ task.title }}</li>
          <input className="checkbox" type="checkbox" v-model="task.completed"/>
        </div>
      </ul>

    </div>
  </div>
</template>

<script>
export default {
  name: 'Todos',
  props: {
    msg: String
  },
  data () {
      return {
      newTask: '',
      idForTask : 0,
      tasks : []
    }
  },
  methods : {
      addTask() {
          if (this.newTask.trim().length == 0) {
              return
          }

          this.tasks.push({
              id: this.idForTask,
              title: this.newTask,
              completed : false,
          })

          this.newTask = ''
          this.idForTask++ 
      },
  }
} 
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.main {
  max-width: 400px;
  margin: 0 auto;
}

.flex {
  display: flex;
}

.flex-center {
  justify-content: center;
}

.space-between {
  justify-content: space-between;
}

.center {
  align-items: center;
}

h1 {
  font-size: 42px;
  display: flex;
  align-self: center;
}

.green {
  color:rgb(111, 255, 176);
}
ul {
  margin: 50px 0;
  padding: 0;
}

ul li {
  background: rgb(111, 255, 176);
  padding: 10px;
  list-style: none;
  width: 81%;
  height: auto;
  margin-bottom: 20px;
}

input.add-task {
  padding: 10px;
  outline: none;
  width: 80%;
  font-size: 14px;
  border: 1px solid rgb(111, 255, 176);
}

button {
  background: rgb(111, 255, 176);
  border: none;
  color: #fff;
  outline: none;
  cursor: pointer;
  font-weight: bold;
  font-size: 16px;
}

input[type=checkbox] {
  position: relative;
    cursor: pointer;
    margin-left: 20px;
    margin-top: 5px;
}
input[type=checkbox]:before {
  content: "";
  display: block;
  position: absolute;
  width: 20px;
  height: 20px;
  top: 0;
  left: 0;
  border: 2px solid #555555;
  border-radius: 3px;
  background-color: white;
}
input[type=checkbox]:checked:after {
  content: "";
  display: block;
  width: 5px;
  height: 10px;
  border: solid black;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
  position: absolute;
  top: 4px;
  left: 8px;
}

.complete {
  text-decoration: line-through;
  background: rgba(111, 255, 176,0.5);
}

</style>