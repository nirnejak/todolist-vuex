<template>
    <div>
        <h3>Todos</h3>
        <div class="legend">
            <span>Double click to mark as complete</span>
            <span>
                <div class="incomplete-box"></div> = Incomplete
            </span>
            <span>
                <div class="complete-box"></div> = Complete
            </span>
        </div>
        <div class="todos">
            <div class="todo" v-for="todo in allTodos" :key="todo.id" @dblclick="onDblClick(todo)" v-bind:class="{'is-complete': todo.completed}">
                {{ todo.title }}
                <i class="material-icons" @click="deleteTodo(todo.id)">delete</i>
            </div>
        </div>
    </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
    name: "Todos",
    methods: {
        ...mapActions(['fetchTodos', 'deleteTodo', 'updateTodo']),
        onDblClick: function(currentTodo) {
            const updatedTodo = {
                id: currentTodo.id,
                title: currentTodo.title,
                completed: !currentTodo.completed
            }

            this.updateTodo(updatedTodo);
        }
    },
    computed: mapGetters(["allTodos"]),
    created() {
        this.fetchTodos();
    }
};
</script>

<style scoped>
.todos {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 1rem;
}

.todo {
    border: 1px solid #ccc;
    background: #41B883;
    padding: 1rem;
    border-radius: 5px;
    text-align: center;
    position: relative;
    cursor: pointer;
}

i {
    position: absolute;
    bottom: 10px;
    right: 10px;
    color: #fff;
    cursor: pointer;
}

.legend {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 1rem;
    margin-bottom: 2rem;
}

.legend span {
    text-align: center;
}

.complete-box {
    display: inline-block;
    width: 10px;
    height: 10px;
    background: #35495E;
}

.incomplete-box {
    display: inline-block;
    width: 10px;
    height: 10px;
    background: #41B883;
}

@media (max-width: 500px) {
    .todos {
        grid-template-columns: 1fr;
    }
    .legend {
        grid-template-columns: 1fr;
    }
}

.is-complete {
    background: #35495E;
    color: #fff
}

</style>