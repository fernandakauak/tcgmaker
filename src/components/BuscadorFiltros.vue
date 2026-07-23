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
  background: #ffffff;
  padding: 12px 14px;
  border-radius: 14px;
  margin-bottom: 16px;
  border: 2px solid #e5e7eb;
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 100%;
  box-sizing: border-box;
}

.seccion-busqueda {
  display: flex;
  align-items: center;
  width: 100%;
}

.input-busqueda {
  width: 100%;
  padding: 8px 12px;
  border: 2px solid #e5e7eb;
  border-radius: 8px;
  font-size: 0.9rem;
  box-sizing: border-box;
  transition: all 0.2s ease;
}

.input-busqueda:focus {
  outline: none;
  border-color: #2374ff;
  box-shadow: 0 0 0 3px rgba(35, 116, 255, 0.1);
}

.seccion-filtros {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  align-items: flex-end;
  width: 100%;
}

.filtro-item {
  display: flex;
  flex-direction: column;
  gap: 3px;
  flex: 1;
  min-width: 90px;
  box-sizing: border-box;
}

.filtro-label {
  font-size: 0.75rem;
  font-weight: 600;
  color: #6b7280;
}

.filtro-select,
.filtro-input {
  padding: 6px 10px;
  border: 2px solid #e5e7eb;
  border-radius: 8px;
  font-size: 0.85rem;
  background: white;
  box-sizing: border-box;
  width: 100%;
  max-width: 100%;
  transition: all 0.2s ease;
}

.filtro-select:focus,
.filtro-input:focus {
  outline: none;
  border-color: #2374ff;
  box-shadow: 0 0 0 3px rgba(35, 116, 255, 0.1);
}

.seccion-limpiar {
  display: flex;
  justify-content: flex-end;
  margin-top: 2px;
}

.btn-limpiar {
  padding: 6px 14px;
  background: #ef4444;
  color: white;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  font-size: 0.8rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn-limpiar:hover {
  background: #dc2626;
  box-shadow: 0 2px 4px rgba(239, 68, 68, 0.3);
}

/* Responsive */
@media (max-width: 600px) {
  .seccion-filtros {
    flex-direction: column;
    gap: 8px;
  }
  
  .filtro-item {
    width: 100%;
  }

  .seccion-limpiar {
    justify-content: center;
  }
}
</style>