<template>
  <main>
    <h2>{{title}}</h2>
    <p>Add day-to-day tasks to be on track.</p>
    <hr/>
    <input type="text" class='taskField' v-model='newTask' v-on:keypress.13='addTask' placeholder='Add a new task ...' />

    <ul v-show='tasks.length' class="data">
      <li v-for="item in tasks" v-bind:class='{ complete : item.isComplete }'>
        <i v-bind:class="item.isComplete ? 'mdi mdi-checkbox-marked-outline' : 'mdi mdi-checkbox-blank-outline' "
          v-on:click='toggleTask(item)' aria-hidden='true' />
        <span v-if='!item.isEditable'>{{ item.list }}</span>
        <input type='text' v-else v-model='item.list' @keyup.enter.esc='updateTask(item)'
          @blur='updateTask(item)' class='editField'
          v-bind:autofocus="item.isEditable ? 'autofocus' : 'false' " />
        <span class='btn-actions'>
          <i v-if='!item.isEditable' class='mdi mdi-pencil' v-on:click='editTask(item)' aria-hidden='true' />
          <i v-else class='mdi mdi-update' v-on:click='updateTask(item)' aria-hidden='true' />
          <i class='mdi mdi-delete' v-on:click='deleteTask(item)' aria-hidden='true' />
        </span>
      </li>
    </ul>

    <p class='markAll'>
      <i>Mark all tasks as complete</i>
      <i v-bind:class="isAllComplete ? 'mdi mdi-checkbox-marked' : 'mdi mdi-checkbox-blank' "
        v-on:click='toggleComplete' aria-hidden='true' />
    </p>
  </main>
</template>

<script>
  export default {
    name: 'ToDoList',
    data () {
      return {
        newTask: '',
        isAllComplete: false,
        title: 'My Task List',
        tasks: [
          { list: 'Check mails', isComplete: true, isEditable: false },
          { list: 'Apply for leave', isComplete: false, isEditable: false }
        ]
      }
    },
    methods: {
      // This method adds tasks to the list
      addTask: function() {
        if(this.newTask.trim())
          this.tasks.push({
            list: this.newTask.trim(),
            isComplete: false,
            isEditable: false
          });
        this.newTask = '';
        this.isAllComplete = false;
      },
      // This method deletes the task from the list
      deleteTask: function(task) {
        this.tasks.splice(this.tasks.indexOf(task), 1);
      },
      // This method enables us to check / uncheck the added tasks
      toggleTask: function(task) {
        this.tasks[this.tasks.indexOf(task)].isComplete = !task.isComplete;
      },
      // This method enables us to edit the added tasks
      editTask: function(task){
        this.tasks.forEach(t => { t.isEditable = false });
        this.tasks[this.tasks.indexOf(task)].isEditable = !task.isEditable;
      },
      // This method updates the added tasks
      updateTask: function(task) {
        this.tasks[this.tasks.indexOf(task)].isEditable = false;
        if(!task.list.trim())
          this.tasks.splice(this.tasks.indexOf(task), 1);
      },
      // This method enables us to check / uncheck all tasks complete
      toggleComplete: function() {
        this.isAllComplete = !this.isAllComplete;
        this.tasks.forEach( t => { t.isComplete = this.isAllComplete });
      }
    }
  }
</script>

<style scoped>
main {
  width: 60%;
  margin: 0 auto;
}

h2 {
  margin-bottom: 5px;
}

p {
  margin: 0;
}

hr {
  margin: 5px 0 30px;
}

.taskField {
  width: 100%;
  border-radius: 5px;
  padding: 10px;
  outline: 0;
  border: 1px solid grey;
}

.taskField:focus {
  box-shadow: 0 0 5px #2c5973;
}

ul {
  list-style-type: none;
  padding: 0;
}

.editField {
  background-color: #ffffff36;
  border: 1px solid transparent;
  color: white;
  padding: 7px;
  margin: -6px 2px;
  font-style: italic;
}

li {
  font-size: 18px;
  padding: 10px 5px;
  margin-bottom: 3px;
  background-color: #519fcc;
  transition: all 0.8s ease-out;
}

li.complete {
  opacity: 0.5;
}

i {
  cursor: pointer;
}

.btn-actions {
  display: none;
  float: right;
}

.btn-actions  i:hover {
  box-shadow: 0 0 5px #FFF;
}

li:hover .btn-actions {
  display: inline;
}

p.markAll {
  text-align: right;
  margin: 40px 0 10px;
}

@media (max-width: 768px) {
  main {
    width: 90%;
  }
}
</style>
