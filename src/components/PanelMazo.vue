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
        cartasDisp.value = cartasDisp.value.filter(crd => crd.id !== id)
    };

    function agregarCarta(elegida) {
        const existe = cartas.find(disponible => disponible.id === elegida.id)
        if (existe) {
            existe.cantidad++
        } else {
            cartas.push({ ...elegida, cantidad: 1 })
        }
    };

</script>

<template>
    <StatsMazo 
        v-for="parte in mazo.cartas"
        :key="parte.id"
        :card="parte"
        @eliminar="borrarCarta"
    />
    <section>
        <CartaMazo 
            v-for="carta in cartasDisp"
            :key="carta.id"
            :card="carta"
            @sumar="agregarCarta"
        />
    </section>
</template>

<style></style>