<template>
  <div class="back">
    <intro></intro>
    <pwd /><cmd />
  </div>
</template>

<script>
import intro from './components/intro'
import cmd from './components/cmd'
import pwd from './components/pwd'

export default {
  components: {
    intro,
    cmd,
    pwd
  },
}
</script>

<style scoped>
.back {
  padding: 10px; 
  background-color: #000;
  min-height: 100vh;
}
</style>