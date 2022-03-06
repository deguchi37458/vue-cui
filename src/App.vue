<template>
  <div class="back">
    <intro></intro>
    <div id="wrapper">
      <ul>
        <li v-for="item in items" v-bind:key="item.id">
          <div><p class="pass-pwd">{{item.pass_pwd}}</p><p class="pass-cmd">{{item.pass_cmd}}</p></div>
          <help v-if="item.pass_cmd == 'help'"></help>
          <about v-else-if="item.pass_cmd == 'cat about.txt'"></about>
          <skill v-else-if="item.pass_cmd == 'cat skill.txt'"></skill>
          <span v-else-if="item.pass_cmd == 'ls'" v-for=" ls in lss" v-bind:key="ls.id">{{ls}}</span>
          <p v-else-if="item.pass_cmd == 'date'">{{item.pass_date}}</p>
          <p v-else-if="item.pass_cmd == 'history'" v-for="history in item.pass_histories" v-bind:key="history.id">{{history}}</p>
          <p class="error" v-else>{{item.pass_cmd}}：Command not found.  Use 'help' to see the command list.</p>
        </li>
      </ul>
    </div>
    <p class="pwd" v-text="pwd"></p>
    <input class="cmd" type="text" v-model="cmd" v-on:keydown.enter="onEnter" v-on:keydown.up="onUp" style="ime-mode:disabled;" >
  </div>
</template>

<script>
import intro from './components/intro'
import help from './components/help'
import about from './components/about'
import skill from './components/skill'

export default {
  components: {
    intro,
    help,
    about,
    skill
  },
  data: function(){
    return {
      judge:'',
      pwd:'hirokideguchi $',
      cmd:'',
      items:[],
      histories:[],
      lss:['about.txt', 'skill.txt']
    }
  },
  methods: {
    onEnter: function(){
      if(this.cmd == 'clear'){
        this.items = [];
      }else{
        this.judge = this.cmd;
        this.histories.push(this.cmd);
        this.items.push({
          pass_pwd: this.pwd,
          pass_cmd: this.cmd,
          pass_histories: this.histories.concat(),
          pass_date: this.date_gen()
        })
      }
      this.cmd = '';
    },
    date_gen: function(){
      let date = new Date;
      let aryWeek = ['日', '月', '火', '水', '木', '金', '土'];
      this.date = date.getFullYear() + '年　' +(date.getMonth() + 1) + '月　' + date.getDate() + '日　' + aryWeek[date.getDay()] + '曜日　' + date.getHours() + '時' + date.getMinutes() + '分' + date.getSeconds() + '秒　JST';
      return this.date
    },
  }
}
</script>

<style scoped>
#wrapper {
  color: #fff;
}
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
}
input.cmd {
  color: #fff;
  font-family: 'Space Mono','monospace','Noto Sans JP',sans-serif;
}
span {
  display: inline-block;
  width: 160px;
}
</style>