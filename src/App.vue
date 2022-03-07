<template>
  <div class="back">
    <intro></intro>
    <div id="wrapper">
      <ul>
        <li v-for="item in items" v-bind:key="item.id">
          <div><p class="pass-pwd">{{item.pass_pwd}} $</p><p class="pass-cmd">{{item.pass_cmd}}</p></div>
          <help v-if="item.pass_cmd == 'help'"></help>
          <about v-else-if="item.pass_cmd == 'cat about.txt'"></about>
          <skill v-else-if="item.pass_cmd == 'cat skill.txt'"></skill>
          <p v-else-if="item.pass_cmd == 'date'">{{item.pass_date}}</p>
          <p v-else-if="item.pass_cmd == 'pwd'">{{pwd}}</p>
          <p v-else-if="item.pass_cmd == 'history'" v-for="(history, index) in item.pass_histories" v-bind:key="history.id"> {{index}} {{history}}</p>
          <span v-else-if="item.pass_cmd == 'ls'">
            <span v-if="item.pass_pwd == 'hirokideguchi'">{{lss}}</span>
            <span v-else-if="item.pass_pwd == 'hirokideguchi/about'" v-for="about in lss.about" v-bind:key="about.id">{{about}}</span>
            <span v-else-if="item.pass_pwd == 'hirokideguchi/work'" v-for="work in lss.work" v-bind:key="work.id">{{work}}</span>
          </span>
          <p v-else-if="item.pass_cmd == 'cd'"></p>
          <p class="error" v-else>{{item.pass_cmd}}：{{error}}</p>
        </li>
      </ul>
    </div>
    <p class="pwd">{{pwd}} $</p>
    <input id="cmd" class="cmd" type="text" v-model="cmd" v-on:keydown.enter="onEnter" v-on:keydown.up="onUp" v-on:keydown.down="onDn" style="ime-mode:disabled;" >
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
      pwd:'hirokideguchi',
      cmd:'',
      items:[],
      histories:[],
      lss:{
        about: ['about.txt', 'skill.txt'],
        work: ['work1.txt', 'work2.txt']
      },
      i:'',
      error:''
    }
  },
  methods: {
    onEnter: function(){
      this.cmd = this.cmd.trim();
      let cmd_sp = this.cmd.split(' ');
      this.histories.push(this.cmd);
      if(this.cmd == 'clear'){
        this.items = [];
      }
      // ディレクトリ移動
      if(cmd_sp[0] == 'cd'){
        if(cmd_sp[1] == '../'){
          this.pwd = 'hirokideguchi'
        }else{
          this.pwd = this.pwd + '/' +cmd_sp[1];
          this.error = 'No such file or directory';
        }
      }
      this.items.push({
        pass_pwd: this.pwd,
        pass_cmd: this.cmd,
        pass_histories: this.histories.concat(),
        pass_date: this.date_gen(),
        pass_error: 'Command not found.  Use `help` to see the command list.'
      })
      console.log("OK");
      this.cmd = '';
      this.i = this.items.length;
    },
    onUp: function(){
      this.cmd = this.items[this.i-1].pass_cmd;
      this.i--;
    },
    onDn: function(){
      this.i++;
      this.cmd = this.items[this.i-1].pass_cmd;
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