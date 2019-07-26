<template lang="pug">
#Todolist
    #todoArea
        p.dateText {{ today }}
        p.font-weight-regular.title.font-italic todo
        p(v-for='todo in todos' ref='todo') {{ todo.content }}
            v-btn(@click='removeTask(todo.uuid)') remove task
        v-flex(xs12)
            v-text-field(label='write your task' hint='example: washing' persistent-hint outline v-model='newTask' @keyup.enter='addNewTask()')
        v-btn(@click='addNewTask()') add tas
        v-btn(@click='drawFrame()') aaa
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
        const task: Task = {
            uuid: uuidv1(),
            content: this.newTask,
        };
        this.todos.push(task);
        this.newTask = '';
    }

    private removeTask(uuid: string) {
        this.todos = this.todos.filter(todo =>  todo.uuid !== uuid);
    }

    private getTodayData() {
        const todayData = new Date();
        const year = todayData.getFullYear();
        const month = todayData.getMonth() + 1;
        const date = todayData.getDate();
        const todayText = month + '月' +  date + '日';
        this.today = todayText;
    }

    private drawFrame() {
        const data: HTMLElement | null = document.getElementById('todoArea');
        if (data === null) { return; }
        if ( this.today === this.today) {
            data.setAttribute('style', 'border: 5px solid #f57c00');
        } else {
            return;
        }
    }

    private mounted() {
        this.getTodayData();
        this.drawFrame();
    }
}
</script>

<style lang="stylus">
#Todolist
    margin: 20px 50px
    height: 85%
#todoArea
    margin: 0 auto
    height: 100%
    width: 30%
    padding: 2em
    border-radius: 10px
    background-color: #f5f5f5
.dateText
    font-size: 25px
</style>
