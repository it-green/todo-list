<template lang="pug">
#Todolist
    p.todayMark.font-weight-bold.font-italic TODAY
    p.dateText {{ today }}
    p todos
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component

export default class Todolist extends Vue {
    private today = '';
    private getTodayData() {
        const todayData = new Date();
        const year = todayData.getFullYear();
        const month = todayData.getMonth() + 1;
        const date = todayData.getDate();
        const todayText = month + '月' +  date + '日';
        this.today = todayText;
    }
    private mounted() {
        this.getTodayData();
    }
}
</script>

<style lang="stylus">
    #Todolist
        margin: 20px 50px
    .todayMark
        font-size: 18px
    .dateText
        font-size: 25px
</style>
