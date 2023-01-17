<template>
  <header class="header">
    <h1 class="main-title">To-Do App</h1>
    <form class="form-task" @submit.prevent="createTask">
      <input
        v-model="newTodos"
        placeholder="pleas Enter Your Task"
        class="task-input"
        type="text"
      />

      <button class="task-btn">Add Task</button>
    </form>
  </header>

  <main class="tasks-warrper">

    <ul>
      <li v-for="item in todos" :key="item.id">
        <p :class="{done:item.completed}">
          {{ item.content }}
        </p>
        <button @click="complete(item)" class="complete-btn">Complete</button>
        <button @click="remove(item)" class="delete-btn">Delete</button>
        <!-- <button @click="edit(item)" class="edit-btn">Edit</button> -->
      </li>
    </ul>
  </main>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const todos = ref([]);
    const newTodos = ref("");


    // create
    function createTask() {


      todos.value.push({
        id: Date.now(),
        content: newTodos.value,
        completed: false,
      });

      newTodos.value = "";
    }

    // remove

    function remove(item) {
      todos.value.splice(todos.value.indexOf(item),1)
    }

    // complete
    function complete(item) {
      item.completed=!item.completed;  
   
    }

    // edit
    // function edit(item) {
      
    // const newEdit =  todos.value.map((val)=>{
    //     return val.id===item.id
    //   })

    //   todos.value =newEdit;
    // }

    console.log(newTodos.value);
    return {
      todos,
      newTodos,
      createTask,
      remove,
      complete,
      // edit,
    };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: monospace;
}
html,
body {
  height: 100%;
}
button {
  cursor: pointer;
}

header.header {
  background-color: #173120;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 50px;
  margin-bottom: 50px;
  position: sticky;
}

.main-title {
  color: #2e9d58;
  font-size: 5rem;
  margin-bottom: 10px;
}

.form-task {
  display: flex;
  align-items: center;
  justify-content: center;
}

.task-input {
  width: 80%;
  height: 50px;
}

.task-input {
  outline: 0px;
}
.task-input[placeholder] {
  font-size: 16px;
}

.task-input:focus {
  outline: 1px solid #2e9d58;
  box-shadow: 0px 0px 15px #2e9d58;
  overflow: unset;
}

.task-btn {
  width: 20%;
  height: 50px;
  font-size: 19px;
  background-color: #2e9d58;
  border: 1px solid #2e9d58;
  color: #fff;
  transition: all 0.3s ease-in-out;
}

.task-btn:hover {
  background-color: #fff;
  border: 1px solid #2e9d58;
  color: #2e9d58;
}

/* main */
main {
  display: flex;
  align-items: center;
  justify-content: center;
}
ul {
  list-style: none;
  width: 70%;
}
li {
  border: 5px solid #2e9d58;
  display: flex;
  align-items: center;
  justify-content: space-around;
  padding: 20px;
}
li p {
  font-weight: 700;
  font-size: 20px;
}

.done {
  text-decoration: line-through;
  color: #2e9d58;
}
li .complete-btn {
  color: #fff;
  font-weight: bold;
  padding: 10px;
  background-color: #2e9d58;
  font-size: 19px;
}

li .delete-btn {
  color: #fff;
  font-weight: bold;
  padding: 10px;
  background-color: #e64533;
  font-size: 19px;
}
li .edit-btn{
  color: #fff;
  font-weight: bold;
  padding: 10px;
  background-color: #a5af3c;
  font-size: 19px;
}
</style>
