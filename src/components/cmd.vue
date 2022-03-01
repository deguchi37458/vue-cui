<template>
    <div>
        <pwd></pwd><input type="text" style="ime-mode:disabled;">
    </div>
</template>

<script>
import pwd from './pwd'

export default {
    components: {
        pwd
    }
}
</script>

<style scoped>
    input {
        color: #fff;
    }
</style>