<script setup>
    import { ref, reactive, computed } from 'vue';
    import CartaMazo from './CartaMazo.vue';
    import StatsMazo from './StatsMazo.vue';

    const mazo = reactive({
        cartas: []
    });

    const cartasDisp = ref([
        { id: 0, nombre: "Pipo Master", emoji: "👨‍🎤", tipo: "Criatura", coste: 3, rareza: "Rara" },
        { id: 1, nombre: "Hechizo hecho en casa", emoji: "🌟", tipo: "Hechizo", coste: 1, rareza: "Común" },
        { id: 2, nombre: "Palabras, palabras palabras", emoji: "☠️", tipo: "Trampa", coste: 8, rareza: "Épica" }
    ]);

    function borrarCarta(id) {
        cartasDisp.value = cartasDisp.value.filter(crd => crd.id !== id);
    };

    function agregarCarta(id) {
        const cartaOriginal = cartasDisp.value.find(c => c.id === id);
        if (!cartaOriginal) return;

        const existe = mazo.cartas.find(c => c.id === id);
        if (existe) {
            if (existe.cantidad < 2) {
                existe.cantidad++;
            }
        } else {
            mazo.cartas.push({ ...cartaOriginal, cantidad: 1 });
        }
    };

</script>

<template>
    <StatsMazo :card="mazo.cartas" />

    <section>
        <CartaMazo 
            v-for="carta in cartasDisp"
            :key="carta.id"
            :card="carta"
            @agregar="agregarCarta"
        />
    </section>
</template>

<style></style>