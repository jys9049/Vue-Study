<template>
    <div class="todoItemContainer">
        <li class="todoItem" v-for="item in todo" :key="item.id">
            <input type="checkbox" name="check" id="check" v-on:click="checkedClick(item.id)"
                v-bind:checked="item.checked" />
            <h3 v-bind:class="{ 'finishText': item.checked }">{{ item.text }}</h3>
            <button v-on:click="deleteClick(item.id)"> X </button>
        </li>
    </div>
</template>

<script>
export default {
    props: ['todo'],
    methods: {
        checkedClick(id) {
            this.$emit('checked', id)
        },
        deleteClick(id) {
            this.$emit('delete', id)
        }
    }
}
</script>

<style scoped>
li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  list-style: none;
}

li>input[type="checkbox"] {
  width: 25px;
  height: 25px;
  border: 1px solid #c9c9c9;
  margin: 0;
}

li>button {
  width: 25px;
  height: 25px;
  background: white;
  border: 1px solid #c9c9c9;
  border-radius: 4px;
}

.finishText {
  color: red;
}
</style>