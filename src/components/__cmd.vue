<template>
    <div>
        <pwd></pwd><input type="text" v-model="cmd" v-on:keydown.enter="onEnter" style="ime-mode:disabled;" >
    </div>
</template>

<script>
import pwd from './pwd'

export default {
    components: {
        pwd
    },
    data: function() {
        return{
            judge:''
        }
    }
}
</script>

<style scoped>
    form{
        display: inline-block;
    }
    input[type="text"] {
        color: #fff;
        width: 50%;
    }
    input[type="submit"] {
        color: #fff;
        opacity: 0;
        display: hidden;
    }
</style>