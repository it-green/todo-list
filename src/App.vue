<template lang="pug">
#app
    v-app
        Header
        Todolist
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Vuetify from 'vuetify';
import Header from '@/components/Header.vue';
import Todolist from '@/views/Todolist.vue';

Vue.use(Vuetify);

@Component({
    components: {
        Header,
        Todolist,
    },
})

export default class App extends Vue {

}
</script>

<style lang="stylus">
@import '~vuetify/src/stylus/main'
</style>
