<template>
  <div class="back">
    <intro></intro>
    <pwd></pwd><input type="text" v-model="cmd" v-on:keydown.enter="onEnter" style="ime-mode:disabled;" >
    <help v-if="judge == 'help'"></help>
  </div>
</template>

<script>
import intro from './components/intro'
import pwd from './components/pwd'
import help from './components/help'

export default {
  components: {
    intro,
    pwd,
    help
  },
  data: function(){
    return {
      judge:'',
      cmd: ''
    }
  },
  methods: {
    onEnter: function(){
      this.judge = this.cmd;
    }
  }
}
</script>

<style scoped>
.back {
  padding: 10px; 
  background-color: #000;
  min-height: 100vh;
}
form{
  display: inline-block;
}
input {
  color: #fff;
}
</style>