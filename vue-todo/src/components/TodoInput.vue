<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo"/>
    <span class="addContainer">
        <button v-on:click="addTodo" class="addBtn">+</button>
    </span>

    <ModalComm v-if="showModal" @close="showModal = false">
        <h3 slot="header">경고!
            <span class="closeModalBtn" @click="showModal = false">X</span>
        </h3>
        <h3 slot="body">아무것도 입력하지 않으셨습니다.</h3>
    </ModalComm>
  </div>
</template>

<script>
import ModalComm from './common/ModalComm.vue';
export default {

    data() {
        return {
            newTodoItem: "",
            showModal: false
        }
    },
    methods: {
        addTodo: function() {
            if(this.newTodoItem !== '') {
                // this.$emit('addTodoItem', this.newTodoItem)
                this.$store.commit('addOneItem', this.newTodoItem.trim())
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput: function() {
            this.newTodoItem = '';
        }
    },
    components: {
        ModalComm: ModalComm
    }
}
</script>

<style scoped>
    input:focus {
        outline: none;
    }
    .inputBox {
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input {
        border-style: none;
        font-size: .9rem;
    }
    .addContainer {
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }
    .addBtn {
        color: white;
        vertical-align: middle;
        font-size: 32px;
        background: none;
        border: none;
    }
</style>