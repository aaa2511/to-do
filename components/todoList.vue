<template>
  <div>
    <div class="list_area">
      <div class="list" v-for="{ message, isCompleted, id } in sortedList" :key="id">
        <div class="todo">
        <button class="checkbox" @click="active(id)">
        </button>
        <div class="text">
        {{message}} {{isCompleted}}
        </div>
        <button class="delete" @click="remove(id)">
          <i class="delicon fa fa-trash-o"></i>
        </button>
        </div>
      </div>
      <div class="controler">
        <div class="left">{{isCompletedCount}} items left</div>
        <div class="buttons">
          <div class="button selected">All</div>
          <div class="button">Active</div>
          <div class="button">Completed</div>
        </div>
        <div type="button" class="clear" @click="ascending = !ascending">Clear Completed</div>
      </div>
    </div>
        <button class="btn" >정렬</button>
        <button class="btn" @click="filter = filter == 'all' ? 'completed' : filter == 'completed' ? 'active' : 'all'">{{filter}}</button>
        
  </div>
</template>

<script>
export default {
  props: {
    list: Array
    },
  data() {
    return {
      ascending: true,
      filter: 'all'
    }
  },
  methods: {
    remove (id) {
      this.$emit('removetodo', id)
    },
    active (id) {
      this.$emit('activetodo', id)
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
  }
}
</script>

<style lang="scss">
  .list_area {
      width: 100%;
      border: 1px solid #D3D3D3;
      .list {
        .todo {
          position: relative;
          height: calc(4vh + 4vw);
          border-bottom: 1px solid #D3D3D3;
          display: flex;
          align-items: center;
          justify-content: center;
          .checkbox {
            width: calc(3vh + 3vw);
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            .icon_area {
              display: flex;
              align-items: center;
              justify-content: center;
              border: 1px solid #EDEDED;
              border-radius: 50%;
              width: calc(2vh + 2vw);
              height: calc(2vh + 2vw);
              .icon {

              }
            }
          }
          .text {
            height: 100%;
            width: calc(100% - 5vh - 5vw);
            padding: 0 calc(1vh + 1vw);
            font-size: calc(2vh + 2vw);
            font-weight: 100;
            background: #FDFDFD;
            display: flex;
            align-items: center;
          }
          .delete {
            position: absolute;
            right: calc(1vh + 1vw);
            .delicon {
              }
          }
        }
      }
      .controler {
        position: relative;
        height: calc(3vh + 3vw);
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        .left {
          position: absolute;
          left: calc(1vh + 1vw);
          font-size: calc(1vh + 1vw);
          color: #8C8C8C;
        }
        .buttons {
          position: absolute;
          display: flex;
          font-size: calc(1vh + 1vw);
          color: #8C8C8C;
          .button {
            margin: 0 calc(.4vh + .4vw);
            padding: calc(.4vh + .4vw) calc(.6vh + .6vw);
          }
          .selected {
            border: 1px solid #E4D7D8;
            border-radius: calc(.3vh + .3vw);
          }
        }
        .clear {
          position: absolute;
          right: calc(1vh + 1vw);
          font-size: calc(1vh + 1vw);
          color: #8C8C8C;
        }
      }
    }
</style>