<template>
    <div class="help">
        <p>CUI Mode</p>
        <p>Basic Command</p>
        <p><br></p>
        <ul>
          <li><dl><dt>cat [file]</dt><dd>&nbsp;:open txt files.</dd></dl></li>
          <li><dl><dt>cd [dir]  </dt><dd>&nbsp;:change directory.</dd></dl></li>
          <li><dl><dt>pwd       </dt><dd>&nbsp;:print working directory.</dd></dl></li>
          <li><dl><dt>ls        </dt><dd>&nbsp;:list segments.</dd></dl></li>
          <li><dl><dt>history   </dt><dd>&nbsp;:command history.</dd></dl></li>
          <li><dl><dt>date      </dt><dd>&nbsp;:show date.</dd></dl></li>
        </ul>
    </div>
</template>

<script>

</script>

<style scoped>
.help {
  color: #fff;
}
dt, dd {
  display: inline-block;
  width: 300px;
}
</style>