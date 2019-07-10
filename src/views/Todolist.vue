<template lang="pug">
#Todolist
    p.todayMark.font-weight-bold.font-italic TODAY
    p.dateText {{ today }}
    p todo
    //- todos -> 複数形
    //- todo -> 単数系
    //- todosの中にあるtodo ということで、todo in todos の方が良い
    p(v-for='todo in todos') {{ todo.content }}
        //- クリックした要素のtodo.uuidをremoveTask関数の引数に渡す
        v-btn(@click='removeTask(todo.uuid)') remove task
    v-layout(row wrap)
        v-flex(xs2)
            v-text-field(label='write your task' hint='example: washing' persistent-hint outline v-model='newTask')
            v-btn(@click='addNewTask()') add task
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
// NOTE: UUID(Universally Unique Identifier)、一意なIDを生成してくれるライブラリ
// https://github.com/kelektiv/node-uuid#readme
import uuidv1 from 'uuid/v1';
// Task interfaceのインポート
import { Task } from '@/types';

@Component
export default class Todolist extends Vue {
    private today = '';
    private newTask: string = '';
    private todos: Task[] = [];
    private addNewTask() {
        // newTaskに記入がない場合のチェック
        // 関数の頭でチェックしてしまえば、無駄な処理を走らせなくて済む
        if (this.newTask === '') { return; }

        // 一意なuuidを持つtaskを作成
        const task: Task = {
            uuid: uuidv1(),
            content: this.newTask,
        }

        // 上で生成したtaskをtodos配列にpush
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
        this.todos.splice(0);
    }

    private removeTask(uuid: string) {
        console.log(`uuidが${uuid}のtaskを削除`);
        /**
         * removeTask関数実行時に渡されたuuidのtaskを、this.todosから除外してthis.todosに除外された結果を再代入
         */
        this.todos = this.todos.filter(todo => todo.uuid !== uuid);

        /**
         * 上記のfilterについて省略せず書くと、以下の通り
         * filterに関するドキュメントはこちら -> https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
         */
        // this.todos = this.todos.filter(function(todo) {
        //     return todo.uuid !== uuid;
        // });
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
