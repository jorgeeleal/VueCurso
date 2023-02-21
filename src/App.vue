<script setup>

// --  ref: Reactividad - DOM 
// -- computed: calcular y mostrar valores en función de un valor
import {ref, computed} from 'vue';
import BlogPost from './components/BlogPost.vue';

//--------------------------------------------
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

//------------------------------------------
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
</script>

<template>
  <h1>{{name.toUpperCase()}}</h1> <!-- {{ JS }}-->
  <br>
  <h2>Práctica 1</h2>
  <br>
  <p style="margin-bottom: 10px;">Contador : </p>
  <p :class="classCounter">{{ counter }}</p>  
  <div class="btn-group">
    <button @click="increment" class="btn btn-success">Incrementar</button>
    <button @click="decrement" class="btn btn-danger">Decrementar</button>
    <button @click="reset" class="btn btn-secondary">Recetear</button>
    <button @click="anadir(counter)" :disabled="classArray" class="btn btn-primary">Añadir a favoritos</button>
  </div>
  <br>
  <ul class="list-group mt-2">
    <li
    class="list-group-item"
    v-for="(num, index) in listaFavoritos"
    :key="index"
    >
    {{ num }}
    </li>
  </ul>
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
  <hr>
  <hr>
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