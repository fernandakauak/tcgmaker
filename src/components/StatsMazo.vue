<script setup>
    import { ref, reactive, computed } from 'vue';

    const props = defineProps({
        card: { type: Array, required: true }
    });

    const emit = defineEmits(['ajustar', 'eliminar', 'agregar']);
    const borrar = () => emit('eliminar', props.card.id);
    const sumar = () => emit('agregar', props.card.id);
</script>

<template>
    <p v-if="!card || card.length === 0">No hay cartas en tu baraja. ¡Prueba agregando una!</p>

    <div v-else>
        <h3 v-for="item in card" :key="item.id">
            {{ item.nombre }} <span>{{ item.emoji }}</span> (x{{ item.cantidad }}) <strong>{{ item.coste }}</strong> {{ item.tipo }} - {{ item.rareza }}
        </h3>
    </div>
</template>

<style></style>