<template>
<form @submit.prevent="addNewToDo">
    <h1>ToDo App</h1>
    <input required v-model="newTodo" type="text" name="new todo" placeholder="Add your new todo">
    <div class="button">
        <button type="submit" class="add">Add New ToDo</button>
        <button type="button" class="allDone" @click="markAllDone">Mark all Done</button>
        <button type="button" class="clearAll" @click="clearAll">Clear All</button>
    </div>

    <!-- <h2>{{ newTodo }}</h2> -->
    <div class="todolist">
        <ul>
            <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
                <h2 :class="{ done: todo.done }" @click="toggleDone(todo)">{{ todo.content }}</h2>
                <button @click="removeTodo(index)">Delete</button>
            </li>
        </ul>
    </div>
</form>
</template>

<script>
import {
    ref
} from 'vue'

export default {
    //using composition API

    setup() {
        const newTodo = ref('');
        const todos = ref([]);

        function addNewToDo() {
            todos.value.push({
                id: Date.now(),
                done: false,
                content: newTodo.value,
            });
            newTodo.value = '';
        }

        function toggleDone(todo) {
            todo.done = !todo.done;
        }

        function removeTodo(index) {
            todos.value.splice(index, 1);
        }

        function markAllDone() {
            todos.value.forEach((todo) => todo.done = true);
        }

        function clearAll() {
            todos.value = [];

        }

        return {
            addNewToDo,
            newTodo,
            todos,
            toggleDone,
            removeTodo,
            markAllDone,
            clearAll,
        }
    }

}
</script>

<style>
form {
    width: 40%;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-content: center;
    justify-content: center;
    background-color: white;
    margin: auto;
    border-radius: 20px;
    margin-top: 90px;
    background-color: beige;
}

form input {
    margin-bottom: 2rem;
    padding: 10px;
}

form button {
    margin-bottom: 1rem;
}

body {
    /* background-color: aqua; */
    background:linear-gradient(45deg, red, blue);

}

.add,
.allDone,
.clearAll {
    display: flex;
    gap: 1rem;
    align-content: center;
    justify-content: center;
    flex-wrap: wrap;
    width: 100px;
    background-color: blueviolet;
    color: white;
    cursor: pointer;

}

.button {
    display: flex;
    gap: 1rem;

}

.todolist {
    display: flex;
}

.todolist ul {
    width: 80%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    justify-content: flex-start;

}

.todolist li {
    background-color: white;
    width: 100%;
    display: flex;
    justify-content: space-between;
    justify-content: flex-start;
    margin: auto;
    gap: 1 rem;
    border: 1px solid black;
    gap: 1rem;
    padding-left: 20px;
}

.todolist button {
    background-color: red;
    display: flex;
    width: 50px;
    margin: auto;
    justify-content: flex-end;
}

.done {
    text-decoration: line-through;
}

.todo {
    cursor: pointer;
}
</style>
