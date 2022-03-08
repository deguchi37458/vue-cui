<template>
  <div class="back">
    <intro></intro>
    <div id="wrapper">
      <ul>
        <li v-for="item in items" v-bind:key="item.id">
          <div><p class="pass-pwd">{{item.pass_pwd}} $</p><p class="pass-cmd">{{item.pass_cmd.join(' ')}}</p></div>
          <div v-if="item.pass_error == ''" >
            <help v-if="item.pass_cmd == 'help'"></help>
            <about v-else-if="item.pass_cmd == 'cat about.txt'"></about>
            <skill v-else-if="item.pass_cmd == 'cat skill.txt'"></skill>
            <p v-else-if="item.pass_cmd == 'date'">{{item.pass_date}}</p>
            <p v-else-if="item.pass_cmd == 'pwd'">{{pwd}}</p>
            <p v-else-if="item.pass_cmd == 'history'" v-for="(history, index) in item.pass_histories" v-bind:key="history.id"> {{index}} {{history}}</p>
            <div v-else-if="item.pass_cmd == 'ls'">
              <p v-if="item.pass_pwd == 'hirokideguchi'" >
                <span v-for="key in Object.keys(lss)" v-bind:key="key.id">{{key}}</span>
              </p>
              <span v-else-if="item.pass_pwd == 'hirokideguchi/about'" v-for="about in lss.about" v-bind:key="about.id">{{about}}</span>
              <span v-else-if="item.pass_pwd == 'hirokideguchi/work'" v-for="work in lss.work" v-bind:key="work.id">{{work}}</span>
            </div>
            <p v-else-if="item.pass_cmd[0] == 'cd'"></p>
          </div>
          <p class="error" v-else>{{item.pass_cmd.join(' ')}}：{{item.pass_error}}</p>
        </li>
      </ul>
    </div>
    <p class="pwd">{{pwd}} $</p>
    <input id="cmd" class="cmd" type="text" v-model="cmd" v-on:keydown.enter="onEnter" v-on:keydown.up="onUp" v-on:keydown.down="onDn" autocomplete="off">
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
      error:'',
      availables: ['cd', 'cat', 'ls', 'date', 'help', 'history', 'clear']
    }
  },
  methods: {
    onEnter: function(){
      this.cmd = this.cmd.trim();
      this.cmd = this.cmd.split(' ');
      this.histories.push(this.cmd.join(' '));
      if(this.cmd == 'clear'){
        this.items = [];
      }
      // ディレクトリ移動
      if(this.cmd[0] == 'cd'){
        if(this.cmd[1] == '../' || this.cmd[1] == null){
          this.pwd = 'hirokideguchi'
        }else if(Object.keys(this.lss).includes(this.cmd[1])){
          this.pwd = this.pwd + '/' +this.cmd[1];
        }else{
          this.error = 'No such file or directory';
        }
      }
      // 使用可能なコマンドか
      if(!this.availables.includes(this.cmd[0])){
        this.error = 'Command not found.  Use `help` to see the command list.'
      }
      this.items.push({
        pass_pwd: this.pwd,
        pass_cmd: this.cmd,
        pass_histories: this.histories.concat(),
        pass_date: this.date_gen(),
        pass_error: this.error
      })
      // 初期化
      this.cmd = '';
      this.error = '';
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