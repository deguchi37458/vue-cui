<template>
    <div class="about">
        <ul>
            <li><dl><dt>名前    </dt><dd>&nbsp;：出口裕樹</dd></dl></li>
            <li><dl><dt>生年月日</dt><dd>&nbsp;：1994/05/07</dd></dl></li>
            <li><dl><dt>Email   </dt><dd>&nbsp;：deguchi37458@gmail.com</dd></dl></li>
        </ul>
    </div>
</template>

<script>

</script>

<style scoped>
.about {
    color: deepskyblue;
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