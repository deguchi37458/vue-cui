<template>
  <div class="back">
    <intro></intro>
    <div id="wrapper">
      <ul>
        <li v-for="item in items" v-bind:key="item.id">
          <div><p class="pass-pwd">{{item.pass_pwd}}</p><p class="pass-cmd">{{item.pass_cmd}}</p></div>
          <help v-if="item.pass_cmd == 'help'"></help>
          <about v-if="item.pass_cmd == 'cat about.txt'"></about>
          <date v-if="item.pass_cmd == 'date'"></date>
        </li>
      </ul>
    </div>
    <p class="pwd" v-text="pwd"></p>
    <input class="cmd" type="text" v-model="cmd" v-on:keydown.enter="onEnter" style="ime-mode:disabled;" >
  </div>
</template>

<script>
import intro from './components/intro'
import help from './components/help'
import about from './components/about'
import date from './components/date'

export default {
  components: {
    intro,
    help,
    about,
    date
  },
  data: function(){
    return {
      judge:'',
      pwd:'hirokideguchi $',
      cmd:'',
      items:[],
    }
  },
  methods: {
    onEnter: function(){
      if(this.cmd == 'clear'){
        this.items = [];
      }else{
        this.judge = this.cmd;
        this.items.push({
          pass_pwd: this.pwd,
          pass_cmd: this.cmd 
        })
      }
      this.cmd = '';
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
.pwd,
.pass-pwd {
  display: inline-block;
  color: yellow;
  margin-right: 10px;
}
.pass-cmd {
  display: inline-block;
  color: #fff;
}
input.cmd {
  color: #fff;
  font-family: 'ＭＳ ゴシック',sans-serif;
}
</style>