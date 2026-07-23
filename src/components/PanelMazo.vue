<script setup>
    import { ref, computed } from 'vue';
    import CartaMazo from './CartaMazo.vue';
    import StatsMazo from './StatsMazo.vue';

    const cartasDisp = ref([
        { id: 0, nombre: "Pipo Master", emoji: "👨‍🎤", tipo: "Criatura", coste: 3, rareza: "Rara" },
        { id: 1, nombre: "Hechizo hecho en casa", emoji: "🌟", tipo: "Hechizo", coste: 1, rareza: "Común" },
        { id: 2, nombre: "Palabras, palabras palabras", emoji: "☠️", tipo: "Trampa", coste: 8, rareza: "Épica" }
    ]);

    /*function ajustarCarta(id) {
        const c = tareas.value.find(crd => crd.id === id);
        if (c) c.hecha = !c.hecha;
    }*/

    function borrarCarta(id) {
        cartasDisp.value = cartasDisp.value.filter(crd => crd.id !== id)
    }

</script>

<template>
    <CartaMazo 
        v-for="carta in cartasDisp"
        :key="carta.id"
        :card="carta"
        @eliminar="borrarCarta"
    />
    <StatsMazo />

</template>

<style></style>