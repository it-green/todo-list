<template lang="pug">
#Todolist
    #todoArea(ref='todoArea')
        .listHead
            p.dateText.font-weight-bold {{ today }}
        p.content-name.font-weight-bold.title.font-italic todo
        .my-tasks
            .todo-card(v-for='todo in todos')
                p.my-task {{ todo.content }}
                .rem-button-parent
                    v-btn(@click='removeTask(todo.uuid)' color='error') remove task
        .input-area
            .input-area-child
            v-text-field.task-write(label='write your task' hint='example: washing' persistent-hint outline v-model='newTask')
            v-btn(@click='addNewTask()' color='success') add task
</template>

<script lang="ts">
import { Vue, Component, Watch } from 'vue-property-decorator';
import uuidv1 from 'uuid/v1';
import { Task } from '@/types';
import { watch, futimes } from 'fs';

@Component

export default class Todolist extends Vue {
    private today = '';
    private newTask: string = '';
    private todos: Task[] = [];
    private STORAGE_KEY = 'green-todolist';
    private todoStorage = {};

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
        if ( this.today === this.today) {
            (this.$refs.todoArea as HTMLElement).setAttribute('style', 'border: 5px solid #f57c00');
        } else {
            return;
        }
    }

    private mounted() {
        this.getTodayData();
        this.drawFrame();
    }

    // @Watch('todos')
    //     private saveStorage(todos: object) {
    //         this.
    //     }
}
</script>

<style lang="stylus">
#Todolist
    margin: 50px
#todoArea
    margin: 0 auto
    width: 20em
    height: 600px
    border-radius: 10px
    background-color: #f5f5f5
.listHead
    height: 3em
    width: 100%
    border-bottom: solid 3px #4CAF50
.dateText
    margin: 0.3em 0 0 0.3em
    font-size: 25px
    color: #757575
.my-tasks
    overflow: scroll
    height: 65%
.todo-card
    background-color: #E0E0E0
    border-top: 0.5px solid #BDBDBD
    border-bottom: 0.5px solid #BDBDBD
.rem-button-parent
    text-align: right
    padding-right: 0.3em
.content-name
    margin: 1em 0 1em 0.3em
    color: #757575
.my-tasks
    word-wrap: break-word
    height: 55%
    margin-bottom: 1em
.my-task
    margin: 0.4em 0.5em 0 0.5em
.input-area
    max-width: 90%
    text-align: right
    margin: 0 auto
</style>
