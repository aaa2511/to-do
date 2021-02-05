<template>
    <div class="footer">
        <div>Double-click to edit a todo</div>
        <div>Designed by <span>petehunt</span></div>
        <div>Part of <span>TodoMVC</span></div>
    </div>
</template>

<script>
export default {

}
</script>

<style lang="scss">
.footer {
    margin-top: calc(4vh + 4vw);
    text-align: center;
    div {
      margin-bottom: calc(.5vh + .5vw);
      font-size: calc(.8vh + .8vw);
      color: #DAD7D8;
      font-weight: 100;
    }
    span {
      color: #BBBCBC;
      font-weight: bold;
    }
  }
</style>