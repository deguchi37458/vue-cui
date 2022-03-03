<template>
    <div class="date">
        <p>{{date}}</p>
    </div>
</template>

<script>

// let date = new Date;
// let text = '';
// let aryWeek = ['日', '月', '火', '水', '木', '金', '土'];
// text = date.getFullYear() + '年' +(date.getMonth() + 1) + '月' + date.getDate() + '日' +'(' + aryWeek[date.getDay()] + ')' + date.getHours() + '時' + date.getMinutes() + '分' + date.getSeconds() + '秒';

export default {
    data: function(){
        return {
            date: ''
        }
    },
    methods: {
        date_gen: function(){
            let date = new Date;
            let aryWeek = ['日', '月', '火', '水', '木', '金', '土'];
            this.date = date.getFullYear() + '年' +(date.getMonth() + 1) + '月' + date.getDate() + '日' +'(' + aryWeek[date.getDay()] + ')' + date.getHours() + '時' + date.getMinutes() + '分' + date.getSeconds() + '秒';
            return date;
        }
    }
}
</script>

<style scoped>
.date {
    color: #fff;
}
</style>