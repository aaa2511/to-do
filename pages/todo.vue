<template>
<div class="page_area">
  <todo-header />
  <div class="input_and_list">
    <todo-input @inputList="fromInput" />
    <todo-list :list="list" @removetodo="remove" @activetodo="active" />
  </div>
  <todo-footer />
  <link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
</div>
</template>

<script>
import TodoFooter from '../components/todoFooter.vue'
import todoHeader from '../components/todoHeader.vue'
import todoInput from '../components/todoInput'
import TodoList from '../components/todoList.vue'

export default {
  data() {
    return {
      list: []
    }
  },
  components: { 
    todoHeader,
    todoInput,
    TodoList,
    TodoFooter
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

<style lang="scss">
.page_area {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  flex-direction: column;
  background: #F3F3F3;
  .input_and_list {
    box-shadow: 0px calc(.5vh + .5vw) calc(1vh + 1vw) calc(1vh + 1vw) rgba(0, 0, 0, .1);
    width: calc(40vh + 40vw);
    background: #FDFDFD;
  }
}
</style>
