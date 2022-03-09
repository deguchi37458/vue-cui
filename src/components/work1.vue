<template>
    <div class="work1">
        <p>Portfolio</p>
        <p><a href="https://deguchihi.net" target="_blank">https://deguchihi.net</a></p>
        <p><br></p>
        <ul>
            <li><dl><dt>使用言語</dt><dd>&nbsp;：HTML/CSS, JavaScript, PHP</dd></dl></li>
            <li><dl><dt>CMS</dt><dd>&nbsp;：WordPress</dd></dl></li>
            <li><dl><dt>ツール</dt><dd>&nbsp;：gsap</dd></dl></li>
        </ul>
    </div>
</template>

<script>

</script>

<style scoped>
.work1 {
    color: deepskyblue;
}
a {
    color: deepskyblue;
    text-decoration: underline;
}
dt {
    display: inline-block;
    width: 160px;
}
dd {
    display: inline-block;
    width: 300px;
}
@media screen and (max-width:480px){
    dt, dd {
        display: block;
        width: 100%;
    }
}
</style>