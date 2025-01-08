<template>
    <Layout>
        <template #header>
            En tête
        </template>
        <template v-slot:aside>
            Sidebar
        </template>
        <template v-slot:main>
            Main
        </template>
        <template v-slot:footer>
            Footer
        </template>
    </Layout>
    <form action="" @submit.prevent="addTodo">
        <fieldset role="group">
            <input v-model="newTodo" type="text" placeholder="Tâche à effectuer">
            <button :disabled="newTodo.length === 0">Ajouter</button>
        </fieldset>
    </form>
  <h1>TODO-LIST</h1>
    <div v-if="todos.length === 0"> Vous n'avez pas de tâches à faire :c </div>
    <div v-else>
        <ul>
            <li
                v-for="todo in sortedTodos"
                :key="todo.date"
                :class="{completed: todo.completed}">
                <Checkbox :label="todo.title"
                          v-model="todo.completed"
                />

            </li>
        </ul>
        <label>
            <input type="checkbox" v-model="hideCompleted">
            Masquer les tâches complétées
        </label>
        <p v-if="remainingTodos > 0">
            {{ remainingTodos }} tâche{{ remainingTodos > 1 ? 's' : '' }} à faire
        </p>
        <Checkbox :label="'Bonjour'"/>
    </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import Checkbox from './Checkbox.vue'
import Button from '@/Button.vue'
import Layout from '@/Layout.vue'

const newTodo = ref('');
const todos = ref([{
    title: 'Tâche 1',
    completed: true,
    date: 1,
},{
    title: 'Tâche 2',
    completed: false,
    date: 2,
}]);

const hideCompleted = ref(false);
const addTodo = () => {
    todos.value.push({
        title: newTodo.value,
        completed: false,
        date: Date.now()
    })
    newTodo.value = '';
}

const sortedTodos = computed(() => {
    console.log('demo')
    const sortedTodos =  todos.value.toSorted((a,b) => a.completed > b.completed ? 1 : -1);
    if (hideCompleted.value === true){
        return sortedTodos.filter(t => t.completed === false)
    }
    return sortedTodos;
})

const remainingTodos = computed(() => {
    return todos.value.filter(t => t.completed === false).length;
})

</script>

<style>
.completed {
    opacity: .5;
    text-decoration: line-through;
}
</style>
