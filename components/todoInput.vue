<template>
  <div>
    <div class="input_area">
      <div class="button"></div>
      <input class="input" @keyup.enter="enter" v-model="message" :placeholder="placeholder">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message : '',
      placeholder: 'What neeeds to be done?'
    }
  },
  methods: {
    enter() {
      this.$emit('inputList', { message: this.message || this.placeholder, id: new Date().getTime(), isCompleted: false })
      this.clearInput()
    },
    clearInput() {
      this.message = ''
    }
  }
}
</script>

<style lang="scss">
.input_area {
      position: relative;
      width: 100%;
      border: 1px solid #D3D3D3;
      height: calc(4vh + 4vw);
      .button {
        float: left;
        width: calc(3vh + 3vw);
        height: 100%;
        background-color: lawngreen;
      }
      .input {
        float: left;
        height: 100%;
        width: calc(100% - 5vh - 5vw);
        border: none;
        padding: 0 calc(1vh + 1vw);
        font-size: calc(2vh + 2vw);
        font-weight: 100;
        background: #FDFDFD;
      }
      .input:focus {
        outline: none;
      }
      .input::placeholder {
        font-weight: 100;
        font-style: italic;
        opacity: .3;
      }
    }
</style>