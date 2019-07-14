<template lang="pug">
#Todolist
    p.todayMark.font-weight-bold.font-italic TODAY
    p.dateText {{ today }}
    p todo
    p(v-for='todo in todos' ref='todo') {{ todo.content }}
        v-btn(@click='removeTask(todo.uuid)') remove task
    v-layout(row wrap)
        v-flex(xs2)
            v-text-field(label='write your task' hint='example: washing' persistent-hint outline v-model='newTask' @keyup.enter='addNewTask()')
            v-btn(@click='addNewTask()') add task
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import uuidv1 from 'uuid/v1';
import { Task } from '@/types';

@Component

export default class Todolist extends Vue {
    private today = '';
    private newTask: string = '';
    private todos: Task[] = [];

    private addNewTask() {
        if (this.newTask === '') { return; }
        // taskの生成
        const task: Task = {
            uuid: uuidv1(),
            content: this.newTask,
        };
        this.todos.push(task);
        this.newTask = '';
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
