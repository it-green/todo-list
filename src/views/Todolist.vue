<template lang="pug">
#Todolist
    p.todayMark.font-weight-bold.font-italic TODAY
    p.dateText {{ today }}
    p todo
    p(v-for='list in todos' ref='todo') {{ list.todo }}
        v-btn(@click='removeTask(list)') remove task
    v-layout(row wrap)
        v-flex(xs2)
            v-text-field(label='write your task' hint='example: washing' persistent-hint outline v-model='newTask' @keyup.enter='addNewTask()')
            v-btn(@click='addNewTask()') add task
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component

export default class Todolist extends Vue {
    private today = '';
    private newTask: string = '';
    private todos = [{}];
    private addNewTask() {
        const task = this.newTask;
        if (task === '') {
            return;
        } else {
            this.todos.push( { todo: this.newTask } );
            this.newTask = '';
        }
    }
    private removeTask(list: string) {
        const index = this.todos.indexOf(list);
        this.todos.splice(index, 1);
    }
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
        this.todos.splice(0);
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
