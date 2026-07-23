<script setup>
import { computed } from 'vue';
import CartaMazo from './CartaMazo.vue';
import StatsMazo from './StatsMazo.vue';

const props = defineProps({
    mazo: { type: Array, default: () => [] }
});

const listaMazo = computed(() => props.mazo);
</script>

<template>
    <div class="panel-mazo">
        <StatsMazo :card="listaMazo" />
    </div>
</template>

<style scoped>
.panel-mazo {
    background: white;
    padding: 16px;
    border-radius: 14px;
    border: 2px solid #e5e7eb;
}
</style>