<template>
    <div class="container grid-xs py-2">
        <span class="label label-primary col-12 image-logo">ToDoList</span>

        <form @submit.prevent="addTodo(todo)">
            <div class="input-group">
                <input
                    type="text"
                    v-model="todo.description"
                    class="form-input"
                    placeholder="Novo todo"
                />
                <button class="btn btn-primary input-group-btn">
                    Adicionar
                </button>
            </div>
        </form>
        <div class="todo-list">
            <Todo
                v-for="t in todos"
                :key="t.id"
                @toggle="toggleTodo"
                :todo="t"
                @remove="removeTodo"
            />
        </div>
    </div>
</template>

<script>
import Todo from "./components/Todo.vue";

export default {
    name: "App",
    components: {
        Todo,
    },
    data() {
        return { todos: [], todo: { checked: false } };
    },
    methods: {
        addTodo(todo) {
            todo.id = Date.now();
            this.todos.push(todo);
            this.todo = { checked: false };
        },

        toggleTodo(todo) {
            const index = this.todos.findIndex((item) => item.id === todo.id);
            if (index > -1) {
                const checked = !this.todos[index].checked;
                (this.todos[index].checked = checked),
                    { ...this.todos[index], checked };
            }
        },

        removeTodo(todo) {
            const index = this.todos.findIndex((item) => item.id === todo.id);
            if (index > -1) {
                this.todos.splice(index, 1);
            }
        },
    },
};
</script>

<style  scoped>
.image-logo {
    margin-bottom: 1rem;
    font-size: 4rem;
    text-align: center;
    border-radius: 12px;
}

.todo-list {
    padding-top: 2rem;
}
</style>
