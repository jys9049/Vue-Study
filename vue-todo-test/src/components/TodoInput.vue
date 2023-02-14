<template>
    <div class="inputContainer">
        <input id="text" type="text" v-model="todoText" v-on:keypress.enter="sendEvent">
        <button v-on:click="sendEvent">add</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            todoText: ''
        }
    },
    methods: {
        sendEvent() {
            if (this.todoText.match(/\s/g) || this.todoText === '') {
                return this.todoText = ''
            }
            this.$emit('addBtnClick', this.todoText)
            this.todoText = ''
        }
    }
}
</script>

<style scoped>
input {
    width: 100%;
    height: 40px;
    border: 1px solid #c9c9c9;
    padding-left: 10px;
}

button {
    position: absolute;
    right: 15px;
    width: 30px;
    height: 30px;
    background: white;
    border: none;
    cursor: pointer;
}
</style>