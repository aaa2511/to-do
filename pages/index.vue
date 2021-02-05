<template>
  <div>
    <todo-input @inputList="fromInput" />
    <todo-list :list="list" @removetodo="remove" @activetodo="active" />
    <link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
  </div>
</template>

<script>
import todoInput from '~/components/todoInput'
import todoList from '~/components/todoList'

export default {
  data() {
    return {
      list: []
    }
  },
  components : {
    todoInput,
    todoList
  },
  methods: {
    fromInput(newlist) {
      this.list.push(newlist)
    },
    remove(id) {
      const index = this.list.findIndex(e => e.id == id)
      this.list.splice(index, 1)
    },
    active(id) {
      const index = this.list.findIndex(e => e.id == id)
      this.$set(this.list, index, { ...this.list[index], isCompleted: !this.list[index].isCompleted })
    }
  }
}
</script>

<style>
body {
  text-align:center;
  font-family: Arial, Helvetica, sans-serif;
  background-color:#f6f6f8;
  }
input {
  border-style:hidden;
  width:200px;
  }
button {
  border-style:groove;
  }
</style>