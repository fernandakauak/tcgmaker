<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
  cartas: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['filtrar']);

const textoBusqueda = ref('');
const filtros = ref({
  tipo: 'todos',
  rareza: 'todos',
  costeMaximo: ''
});

const tiposUnicos = computed(() => {
  const types = new Set();
  props.cartas.forEach(c => types.add(c.tipo));
  return ['todos', ...Array.from(types)];
});

const rarezasUnicas = computed(() => {
  const rarities = new Set();
  props.cartas.forEach(c => rarities.add(c.rareza));
  return ['todos', ...Array.from(rarities)];
});

const aplicarFiltros = () => {
  emit('filtrar', {
    texto: textoBusqueda.value,
    tipo: filtros.value.tipo,
    rareza: filtros.value.rareza,
    costeMaximo: filtros.value.costeMaximo
  });
};
</script>

<template>
  <div class="buscador-filtros">
    <div class="seccion-busqueda">
      <input 
        type="text" 
        v-model="textoBusqueda" 
        @input="aplicarFiltros" 
        placeholder="🔍 Buscar por nombre o habilidad..."
        class="input-busqueda"
      >
    </div>

    <div class="seccion-filtros">
      <div class="filtro-item">
        <label class="filtro-label">Tipo</label>
        <select v-model="filtros.tipo" @change="aplicarFiltros" class="filtro-select">
          <option v-for="tipo in tiposUnicos" :key="tipo" :value="tipo">
            {{ tipo === 'todos' ? 'Todos los tipos' : tipo }}
          </option>
        </select>
      </div>

      <div class="filtro-item">
        <label class="filtro-label">Rareza</label>
        <select v-model="filtros.rareza" @change="aplicarFiltros" class="filtro-select">
          <option v-for="rareza in rarezasUnicas" :key="rareza" :value="rareza">
            {{ rareza === 'todos' ? 'Todas las rarezas' : rareza }}
          </option>
        </select>
      </div>

      <div class="filtro-item">
        <label class="filtro-label">Coste Máx.</label>
        <input 
          type="number" 
          v-model.number="filtros.costeMaximo" 
          @input="aplicarFiltros" 
          placeholder="Ej: 5"
          min="0"
          class="filtro-input"
        >
      </div>
    </div>

    <div v-if="textoBusqueda || filtros.tipo !== 'todos' || filtros.rareza !== 'todos' || filtros.costeMaximo !== ''" 
         class="seccion-limpiar">
      <button @click="textoBusqueda = ''; filtros.tipo = 'todos'; filtros.rareza = 'todos'; filtros.costeMaximo = ''; aplicarFiltros()" 
              class="btn-limpiar">
        🧹 Limpiar filtros
      </button>
    </div>
  </div>
</template>

<style scoped>
.buscador-filtros {
  background: #f9fafb;
  padding: 20px;
  border-radius: 16px;
  margin-bottom: 20px;
  border: 2px solid #e5e7eb;
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.seccion-busqueda {
  display: flex;
  align-items: center;
  gap: 10px;
}

.input-busqueda {
  flex: 1;
  padding: 12px 16px;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  font-size: lakdaksdljaskdaskd;
  transition: all 0.3s ease;
}

.input-busqueda:focus {
  outline: none;
  border-color: #2374ff;
  box-shadow: 0 0 0 4px rgba(35, 116, 255, 0.1);
}

.seccion-filtros {
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
}

.filtro-item {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.filtro-label {
  font-size: 0.85rem;
  font-weight: 600;
  color: #6b7280;
}

.filtro-select,
.filtro-input {
  padding: 10px 14px;
  border: 2px solid #e5e7eb;
  border-radius: 10px;
  font-size: 0.95rem;
  background: white;
  transition: all 0.3s ease;
}

.filtro-select:focus,
.filtro-input:focus {
  outline: none;
  border-color: #2374ff;
  box-shadow: 0 0 0 3px rgba(35, 116, 255, 0.1);
}

.filtro-select {
  min-width: 160px;
}

.filtro-input {
  width: 120px;
}

.seccion-limpiar {
  display: flex;
  justify-content: flex-end;
}

.btn-limpiar {
  padding: 10px 20px;
  background: #ef4444;
  color: white;
  border: none;
  border-radius: 10px;
  font-weight: 600;
  font-size: 0.95rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-limpiar:hover {
  background: #dc2626;
  transform: translateY(-2px);
  box-shadow: 0 4px 6px rgba(239, 68, 68, 0.3);
}

/* Responsive */
@media (max-width: 768px) {
  .seccion-filtros {
    flex-direction: column;
  }
  
  .filtro-select,
  .filtro-input {
    width: 100%;
  }
  
  .seccion-limpiar {
    justify-content: center;
  }
}
</style>