<script setup>
import { ref, computed } from 'vue';
import CartaCatalogo from './CartaCatalogo.vue';
import BuscadorFiltros from './BuscadorFiltros.vue';

const props = defineProps({
  cartas: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['agregar']);

const filtrosState = ref({
  texto: '',
  tipo: 'todos',
  rareza: 'todos',
  costeMaximo: ''
});

const aplicarFiltros = (nuevosFiltros) => {
  filtrosState.value = nuevosFiltros;
};

const cartasFiltradas = computed(() => {
  return props.cartas.filter(carta => {
    const coincideTexto = !filtrosState.value.texto || 
      carta.nombre.toLowerCase().includes(filtrosState.value.texto.toLowerCase()) ||
      (carta.habilidad && carta.habilidad.toLowerCase().includes(filtrosState.value.texto.toLowerCase()));
      
    const coincideTipo = filtrosState.value.tipo === 'todos' || carta.tipo === filtrosState.value.tipo;
    const coincideRareza = filtrosState.value.rareza === 'todos' || carta.rareza === filtrosState.value.rareza;
    const coincideCoste = filtrosState.value.costeMaximo === '' || filtrosState.value.costeMaximo === null || carta.coste <= Number(filtrosState.value.costeMaximo);

    return coincideTexto && coincideTipo && coincideRareza && coincideCoste;
  });
});
</script>

<template>
  <BuscadorFiltros :cartas="cartas" @filtrar="aplicarFiltros" />

  <div class="catalogo-grid">
    <CartaCatalogo 
      v-for="carta in cartasFiltradas" 
      :key="carta.id" 
      :carta="carta" 
      @agregar="emit('agregar', $event)"
    />
  </div>
  <div v-if="cartasFiltradas.length === 0" class="sin-resultados">
    🚫 Ninguna carta coincide con los filtros
  </div>
</template>

<style scoped>
.catalogo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(11rem, 0.3fr));
  gap: 16px;
  padding: 20px;
  box-sizing: border-box;
  background-color: white;
  border-radius: 15px;
}
.sin-resultados {
  padding: 40px 20px;
  text-align: center;
  color: #6b7280;
  font-size: 1.2rem;
}

</style>