<template>
  <h1>Bonjour {{ firstName }}</h1>

  <p :id="`p-${count}`" :class="{active: count > 5}">Compteur : {{ count }} <div v-html="span"></div></p>

  <!-- <div v-show="count >= 5">Bravo vous avez cliqué plus de 5 fois</div> -->
  <div v-if="count >= 5">Bravo vous avez cliqué plus de 5 fois</div>

  <button @click="increment">Incrémenter</button>
  <!-- <button @click="decrement">Décrementer</button> -->
  <button @click="count--">Décrementer</button>
  <hr>
  <button @click="sortMovies">Réorganiser</button>
  <form action="" @submit.prevent="addMovie">
    <input type="text" placeholder="Nouveau film" v-model="movieName">
    <button>Ajouter</button>
  </form>

  <ul>
    <li
      v-for="movie in movies"
      :key="movie"
    >
      {{movie}}
      <button @click="deleteMovie(movie)">Supprimer</button>
    </li>
  </ul>

    <ul>
      <li>
        {{person.firstname}}
      </li>

      <li>
        {{person.lastname}}
      </li>

      <li>
        {{person.age}}
      </li>
    </ul>
    <button @click.prevent="randomAge">
    Changer age
  </button>
  <hr>

</template>
<script setup>
import {ref} from 'vue';

const firstName = "Lilya";
const count = ref(0);
const span = '<span>Demo</span>';

const movieName = ref('');
const movies = ref([
  'Matrix',
  'Lilo & Stitch',
  'Titanic',
]);

const person = ref({
  firstname: 'John',
  lastname: 'Doe',
  age: 28,
});

console.log(count, count.value);
const increment = (event) => {
  console.log(event);
  count.value++;
}

const decrement = () => {
  count.value++;
}

const deleteMovie = (movie) => {
  movies.value = movies.value.filter(m => m !== movie)
}

const sortMovies = () => {
  movies.value.sort((a,b) => a > b ? 1 : -1)
}

const addMovie = () => {
  movies.value.push(movieName.value);
  movieName.value = '';
}

const randomAge = () => {
  person.value.age = Math.round(Math.random()* 100);
}

</script>

<style>
h1{
  color: red;
}
.active {
  color: red;
}
</style>
