<template>
    <div class="inputContainer">
        <input id="text" type="text" v-model="text" v-on:keypress.enter="sendEvent">
        <button v-on:click="addTodo">add</button>
    </div>
</template>

<script>
export default {
    methods: {
        sendEvent() {
            this.$emit('addTodo')
        }
    }
}
</script>

<style>

</style>