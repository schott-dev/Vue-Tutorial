<template>
  <div>
    <p>Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
    <p>Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
    <todo v-on:delete-todo="deleteTodo" v-for="todo in orderedTodos" v-bind:todo="todo" v-bind:key="todo.id"></todo>
    <create-todo v-on:add-todo="addTodo"></create-todo>
  </div>
</template>

<script>
import Todo from './ToDo'
import CreateTodo from './CreateToDo'
export default {
  name: 'ToDoList',
  components: {
    Todo,
    CreateTodo
  },
  data () {
    return {
      todos: [{
        id: 1,
        title: 'Todo A',
        project: 'Project A',
        done: false
      }, {
        id: 4,
        title: 'Todo D',
        project: 'Project D',
        done: true
      }, {
        id: 3,
        title: 'Todo C',
        project: 'Project C',
        done: false
      }, {
        id: 2,
        title: 'Todo B',
        project: 'Project B',
        done: false
      }]
    }
  },
  computed: {
    orderedTodos: function () {
      return _.orderBy(this.todos, 'id')
    }
  },
  methods: {
    deleteTodo (todo) {
      console.log('deleteToDo')
      const todoIndex = this.todos.indexOf(todo)
      this.todos.splice(todoIndex, 1)
    },
    addTodo (title, project) {
      console.log(title, project)
      this.todos.push({
        title,
        project,
        done: false
      })
    }
  }
}
</script>

<style>
</style>
