<template>
<form @submit.prevent="addNewToDo">
    <h1>ToDo App</h1>
    <input required v-model="newTodo" type="text" name="new todo" placeholder="Add your new todo">
    <div class="button">
        <button type="submit" class="add"><img src="./assets/add.svg"></button>
        <button type="button" class="allDone" @click="markAllDone">All Done</button>
        <button type="button" class="clearAll" @click="clearAll">Clear All</button>
    </div>

    <!-- <h2>{{ newTodo }}</h2> -->
    <div class="todolist">
        <ul>
            <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
                <h2 :class="{ done: todo.done }" @click="toggleDone(todo)">{{ todo.content }}</h2>
                <button @click="removeTodo(index)"><img src="./assets/delete.svg"></button>
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
    width: 350px;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-content: center;
    justify-content: center;
    background-color: white;
    margin: auto;
    border-radius: 20px;
    margin-top: 10rem;
    padding: 0.5rem;
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
    height:100vh;

}

.add,
.allDone,
.clearAll {
    display: flex;
    gap: 1.5rem;
    align-content: center;
    justify-content: center;
    flex-wrap: wrap;
    width: 100px;
    background-color: blueviolet;
    color: white;
    cursor: pointer;
    padding:0.5rem;

}

.button {
    display: flex;
    gap: 1rem;

}

.todolist {
    display: flex;
}

.todolist ul {
    width: 100%;
    display: flex;
    flex-direction: column;
    padding:0;
    gap:10px;

}

.todolist li {
    background-color: rgb(247, 245, 245);
    width: 100%;
    margin: auto;
    border: 1px ;
    display:flex;
    justify-content: space-between;


}
 
.todolist h2{
    padding: 10px;
    margin: 10px;
}

.todolist button:hover{
    background-color:rgb(208, 43, 43);
}

.todolist button {
    padding: 10px;
    margin: 10px;
    /* background-color: red;
    display: flex;
    width: 50px;
    margin: auto;
    justify-content: flex-end; */
}

.done {
    text-decoration: line-through;
}

.todo {
    cursor: pointer;
}
</style>
