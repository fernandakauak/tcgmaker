<script setup>
    import { ref, computed } from 'vue';

    const emit = defineEmits(['ajustar', 'quitar']);
    
    defineProps({
        card: { type: Object, required: true}
    });
</script>

<template>
    <section>
        <div>
            <h1> {{ card.nombre }} <span>{{ card.emoji }}</span> <strong>{{ card.coste }}</strong></h1>
            <h2>{{ card.tipo }}</h2>
            <h3>{{ card.rareza }}</h3>
        </div>
    </section>
</template>

<style></style>