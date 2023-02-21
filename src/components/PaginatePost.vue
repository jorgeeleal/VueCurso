<script setup>

defineProps(['inicio', 'fin', 'apilenght']);

</script>

<template>
    <div class="btn-group mb-3" role="group" aria-label="pagination">
        <button @click="$emit('previos')" 
        type="button" 
        class="btn btn-outline-primary"
        :disabled="inicio <= 0"
        >Anterior</button>

        <button @click="$emit('siguientes')" 
        type="button" 
        class="btn btn-outline-primary"
        :disabled="fin >= apilenght"
        >Siguiente</button>
    </div>
</template>