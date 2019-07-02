<template lang="pug">
#app
    v-app
        v-toolbar-title.headline(text-uppercase)
            span Vuetify
        .button-area
            v-btn(color="success") hello
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Vuetify from 'vuetify';
import HelloWorld from './components/HelloWorld.vue';

Vue.use(Vuetify);

@Component({
    components: {
        HelloWorld,
    },
})

export default class App extends Vue {}
</script>

<style lang="stylus">
@import '~vuetify/src/stylus/main'
</style>
