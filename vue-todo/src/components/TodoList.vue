<template>
    <div>
        <ul>
            <li v-for="(todoItem, index) in this.todoItems" v-bind:key="index" class="shadow">
                <span class="checkBtn" :class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleCompleted(todoItem)">V</span>
                <span :class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
                <span class="removeBtn" v-on:click="removeTodo({...todoItem.item, index})">
                    X
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex'

export default {
    methods: {
        ...mapMutations({
                removeTodo: 'removeOneItem'
            }),
        removeTodo(todoItem, index) {
            this.$store.commit('removeOneItem', { todoItem, index })
        },
        toggleCompleted (todoItem) {
            // let getItem = JSON.parse(localStorage.getItem(localStorage.key(index)));
            // getItem.completed = !getItem.completed
            // localStorage.setItem(localStorage.key(index), JSON.stringify(getItem))
            // console.log(getItem)
            this.$store.commit('completedOneItem', todoItem)
        }
    },
    computed: {
        // todoItems() {
        //     return this.$store.getters.storedTodoItems
        // }
        ...mapGetters({todoItems: 'storedTodoItems'})
    }
}
</script>

<style scope>
ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}

li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: .5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}

.checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}

.checkBtnCompleted {
    color: #b3adad;
}

.textCompleted {
    text-decoration: line-through;
    color: #b3adad;
}

.removeBtn {
    margin-left: auto;
    color: #de4343;
}
</style>