<template lang="html">
    <li v-on:change="handleChange">{{country.name}}</li>
</template>

<script>

import { eventBus } from '../main';

export default {
    name: "list-component",
    props: ["country"],
    methods: {
        handleChange() {
            eventBus.$emit('country-selected', this.country);
        }
    }
}

</script>

<style>

</style>