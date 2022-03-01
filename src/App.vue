<template>
  <div class="back">
    <intro></intro>
    <cmd /> 
  </div>
</template>

<script>
import intro from './components/intro'
import cmd from './components/cmd'

export default {
  components: {
    intro,
    cmd
  }
}
</script>

<style scoped>
.back {
  padding: 10px; 
  background-color: #000;
  min-height: 100vh;
}
</style>