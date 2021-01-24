<template>
  <div>
      <input @keyup.enter="enter" v-model="message" :placeholder="placeholder">
      <p>메시지 : {{message}} </p>
      <div v-for="{ message, isCompleted, id } in sortedList" :key="id">
        {{message}} {{isCompleted}}
        <button @click="active(id)">완료</button>
        <button @click="remove(id)">삭제</button>
      </div>
      <button @click="ascending = !ascending">정렬</button>
      <button @click="filter = filter == 'all' ? 'completed' : filter == 'completed' ? 'active' : 'all'">{{filter}}</button>
      {{isCompletedCount}} 활성화 갯수
  </div>
</template>

<script>
export default {
  data() {
    return {
      message : '',
      placeholder: '입력해주세요',
      list : [],
      ascending: true,
      filter: 'all'
    }
  },
  computed: {
    filterdList () {
      if (this.filter == 'all') return this.list
      else if (this.filter == 'completed') return this.list.filter(e => e.isCompleted == true)
      else if (this.filter == 'active') return this.list.filter(e => e.isCompleted == false)
    },
    sortedList () {
      return this.filterdList.sort((a, b) => this.ascending ? a.id - b.id : b.id - a.id)
    },
    isCompletedCount () {
      const filterd = this.list.filter(e => e.isCompleted == true)
      return filterd.length
    }
  },
  methods: {
    enter() {
      this.list.push({ message: this.message || this.placeholder, id: new Date().getTime(), isCompleted: false })
    },
    remove (id) {
      const index = this.list.findIndex(e => e.id == id)
      this.list.splice(index, 1)
    },
    active (id) {
      const index = this.list.findIndex(e => e.id == id)
      this.$set(this.list, index, { ...this.list[index], isCompleted: !this.list[index].isCompleted })
    }
  }
}
</script>

<style>

</style>