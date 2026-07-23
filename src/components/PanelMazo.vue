<script setup>
    import { ref, computed } from 'vue';
    import CartaMazo from './CartaMazo.vue';
    import StatsMazo from './StatsMazo.vue';

    defineProps({
        cartas: { type: Object , required: true }
    });

    const cartas = ref([
        { id: 0, nombre: "Pipo Master", emoji: "👨‍🎤", tipo: "Criatura", coste: 3, rareza: "Rara" },
        { id: 1, nombre: "Hechizo hecho en casa", emoji: "🌟", tipo: "Hechizo", coste: 1, rareza: "Común" },
        { id: 2, nombre: "Palabras, palabras palabras", emoji: "☠️", tipo: "Trampa", coste: 8, rareza: "Épica" }
    ]);

</script>

<template>
    <CartaMazo 
        v-for="carta in cartas"
        :key="carta.id"
        :card="carta"
    />
    <StatsMazo />

</template>

<style></style>