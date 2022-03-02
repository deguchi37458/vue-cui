<template>
    <div class="list-watch">
        <span v-for="list in lists" v-bind:key="list.id">{{list}}</span>
    </div>
</template>

<script>


export default {
    data: function(){
        return {
            lists:['about.txt', 'skill.txt']
        }
    }
}
</script>

<style scoped>
.list-watch {
    color: #fff;
}
span {
    display: inline-block;
    width: 200px;
}
</style>