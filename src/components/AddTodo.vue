<template>
    <div>
        <h3>Add Todo</h3>
        <form action="" @submit="onSubmit">
            <input type="text" v-model="title" placeholder="Add Todo">
            <input type="submit" value="Submit">
        </form>
    </div>
</template>

<script>

import { mapActions } from 'vuex';

export default {
    name: "AddTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        ...mapActions(['addTodo']),
        onSubmit(e) {
            e.preventDefault();
            this.addTodo(this.title);
        }
    }
}
</script>

<style scoped>
form {
    display: flex;
}

input[type="text"] {
    flex: 10;
    padding: 10px;
    border: 1px solid #41B883;
    outline: 0;
}

input[type="submit"] {
    flex: 2;
    background: #41B883;
    color: #fff;
    border: 1px #41B883 solid;
    cursor: pointer;
}

</style>
