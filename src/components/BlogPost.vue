<script setup>

defineProps(['id', 'title', 'body', 'colorText']);

//const props = defineProps(['title', 'body', 'colorText']);    -- Acceder a ellos desde <script>

/*
 ** Pasar objetos como props **

    defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: "Sin descripción"  // -- Darle un valor por defecto
        }
    });

*/

//const emit = defineEmits(['cambiarFavorito']);                -- Acceder a emits desde <script>
//emit('funcion', prop)

</script>

<template>
    <div class="card mt-1">
        <div class="card-body">
            <h5 class="card-title">{{id}} - {{title}}</h5>
            <p :class="`text-${colorText}`">{{body}}</p>
            <button @click="$emit('cambiarFavorito', title)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>