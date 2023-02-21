<script setup>

// --  ref: Reactividad - DOM 
// -- computed: calcular y mostrar valores en función de un valor
// -- onMounted: Se ejecuta después de montar el <template>
import {ref, computed, onMounted} from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'

//-------------------------------------------- Practica 1
const name = 'Vue Curso';

const counter = ref(0);
const listaFavoritos = ref([]);

const classArray = computed(() => {
  const existente = listaFavoritos.value.find(num => num === counter.value); //-- retorna el primer valor que cumple || undefined
  return existente || existente === 0;
})

const classCounter = computed(() => {
  if(counter.value === 0) return 'cero';
  if(counter.value < 0) return 'negative';
  if(counter.value > 0) return 'positive';
  return 
})

const increment = () => counter.value++;
const decrement = () => counter.value--;
const reset = () => counter.value = 0;
const anadir = (num) => {
  listaFavoritos.value.push(num);
}

//-------------------------------------------- Practica 2
const posts = ref([
  {
    id: 1,
    title: "Primer post",
    body: "Trabajando con componentes",
    colorText: "primary"
  },
  {
    id: 2,
    title: "Segundo post",
    body: "Utilizando v-for",
    colorText: "primary"
  },
  {
    id: 3,
    title: "Tercer post",
    body: "Este es el tercer elemento",
    colorText: "primary"
  },
  {
    id: 4,
    title: "Cuarto post",
    body: "Cuarto elemento",
    colorText: "secundary"
  }
])

const postFavorito = ref('');
const cambiarFavorito = (post) => {
  postFavorito.value = post;
}
//-------------------------------------------- Practica 3

const apiposts = ref([]);

const loading = ref(true);

/*
  //-- onMounted -- Elemento existente en el DOM

  onMounted(async() => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/posts');
      apiposts.value = await response.json();

    } catch (error) {
      console.log(error);
    } finally {
      setTimeout(() => {                      // -- Solo para visualizar el spinner
        loading.value = false;
      }, 1500);
    }
  })  
*/

const fetchData = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    apiposts.value = await response.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {                  
      loading.value = false;
    }, 1500);
  }
};

fetchData();

const postxpage = 4;
const inicio = ref(0);
const fin = ref(postxpage);

const siguientes = () => {
  inicio.value += postxpage;
  fin.value += postxpage;
}
const previos = () => {
  inicio.value -= postxpage;
  fin.value -= postxpage;
}

</script>

<template>
  <h1 class="mt-3">{{name.toUpperCase()}}</h1> <!-- {{ JS }}-->
  <br>
  <h2>Práctica 1</h2>
  <br>
  <p style="margin-bottom: 10px;">Contador : <span :class="classCounter">{{ counter }}</span></p>
  <br>
  <div class="btn-group">
    <button @click="increment" class="btn btn-success">Incrementar</button>
    <button @click="decrement" class="btn btn-danger">Decrementar</button>
    <button @click="reset" class="btn btn-secondary">Recetear</button>
    <button @click="anadir(counter)" :disabled="classArray" class="btn btn-primary">Añadir a favoritos</button>
  </div>
  <br>
  <div class="container text-start ">
    <ul class="list-group mt-2">
      <li
      class="list-group-item"
      v-for="(num, index) in listaFavoritos"
      :key="index"
      >
      {{ num }}
      </li>
    </ul>
  </div>
  <br>
  <p class="fw-lighter">• (reactividad, eventos, v-if, v-for, computed)</p>
  <br>
  <h2>Práctica 2</h2>
  <br>
  <p>Mi post favorito : {{ postFavorito }}</p> 
  <br>
  <BlogPost
  v-for="post in posts"
  :key="post.id" 
  :id="post.id"
  :title="post.title"
  :body="post.body"
  :colorText="post.colorText"
  @cambiarFavorito="cambiarFavorito"
  />
  <p class="fw-lighter">• (componentes, emit, props)</p>
  <br>
  <hr>
  <hr>
  <h2>Práctica 3</h2>
  <br>
  <div class="container text-center">
    <PaginatePost 
    @siguientes="siguientes"
    @previos="previos"
    :inicio="inicio"
    :fin="fin" 
    :apilenght="apiposts.length"
    />
  </div>
  <br>
  <LoadingSpinner v-if="loading"/>
  <BlogPost
  v-for="post in apiposts.slice(inicio, fin)"
  :key="post.id" 
  :id="post.id"
  :title="post.title"
  :body="post.body"
  :colorText="post.colorText"
  @cambiarFavorito="cambiarFavorito"
  v-else
  />
  <p class="fw-lighter">• (consumir API *fetch, onMounted)</p>
</template>

<style>
button {
  padding: 10px;
}
h1 {
  color: gray;
}
.positive{
  color: green;
}
.negative{
  color: red;
}
.cero{
  color: black;
}
</style>

<!-- v-bind: = : -->
<!-- v-on:   = @ -->