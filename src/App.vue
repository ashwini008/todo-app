<template>
  <div id="app">
    <ToDoList/>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList'

export default {
  name: 'App',
  components: {
    ToDoList
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 70%;
  margin: 5% auto 5%;
  background-color: #207db3;
  color: white;
  padding: 20px;
  box-shadow: 4px 4px 10px dimgrey;
}

@media (max-width: 1024px) and (min-width: 769px) {
  #app {
    width: 75%
  }
}

@media (max-width: 768px) {
  #app {
    width: 100%;
    padding: 15px;
  }
}
</style>
