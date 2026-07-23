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
    <div class="carta">
            <h1>{{ card.nombre }} <span>{{ card.emoji }}</span> <strong>{{ card.coste }}</strong></h1>
            <h2>{{ card.tipo }}</h2>
            <h3>{{ card.rareza }}</h3>
            <button class="btn" @click="sumar">Agregar</button>
        </div>
</template>

<style scoped>
    section {
        width: 100%;
        height: 315px;
        display: flex;
    }

    .carta {
        width: 21%;
        margin: 1%;
        padding: 2%;
        border-radius: 10px;
        border: 2px solid black;
        background-color: moccasin;
        display: inline-block;
    }

    .carta h1 {
        width: 100%;
        font-size: 18px;
        text-align: left;
        background-color: mediumseagreen;
        padding: 2%;
    }

    .carta span {
        font-size: 18px;
        padding: 1%;
    }

    .carta strong {
        font-size: 20px;
        text-align: right;
    }

</style>