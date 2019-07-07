<template lang="pug">
#header
    v-toolbar(flat dark color="teal darken-1")
        v-toolbar-title TODO list
        v-spacer
        v-toolbar-side-icon
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component

export default class Header extends Vue {}
</script>

<style lang="stylus">
</style>
