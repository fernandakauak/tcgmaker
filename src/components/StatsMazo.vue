<script setup>
    import { ref, reactive, computed } from 'vue';

    const props = defineProps({
        card: { type: Object, required: true }
    });
    
    const emit = defineEmits(['ajustar', 'eliminar', 'agregar']);
    //const ajustar = ()=> emit('ajustar', props.card.id); //comprobar
    const borrar = ()=> emit('eliminar', props.card.id);
    const sumar = ()=> emit('agregar', props.card.id);
</script>

<template>
    <p v-if="card.length === 0" key="empty">No hay cartas en tu baraja. ¡Prueba agregando una!</p>

    <div v-else key="card">
        <h3 v-for="card in mazo.cartas" :key="card.id">{{ card.nombre }} <span>{{ card.emoji }}</span> <strong>{{ card.coste }}</strong> {{ card.tipo }} - {{ card.rareza }} <button class="btn" @click="borrar">Borrar</button></h3>
    </div>
</template>

<style></style>