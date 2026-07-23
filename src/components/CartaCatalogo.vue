<script setup>
const props = defineProps({
  carta: {
    type: Object,
    required: true
  }
});

const emit = defineEmits(['agregar']);
</script>

<template>
  <div class="tarjeta-carta" :class="carta.rareza?.toLowerCase()">
    <div class="top-bar">
      <span class="emoji">{{ carta.emoji }}</span>
      <span class="coste">{{ carta.coste }} 🔵</span>
    </div>
    
    <div class="cuerpo">
      <h3 class="nombre">{{ carta.nombre }}</h3>
      <p class="habilidad" v-if="carta.habilidad">🎶 {{ carta.habilidad }}</p>
    </div>

    <div class="tags">
      <span class="tag tipo">{{ carta.tipo }}</span>
      <span class="tag rareza">{{ carta.rareza }}</span>
    </div>

    <button class="btn-add" @click="emit('agregar', carta)">+ Agregar</button>
  </div>
</template>

<style scoped>
.tarjeta-carta {
  border-radius: 12px;
  padding: 14px;
  background: #ffffff;
  border: 2px solid #ddd;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 5px;
  box-sizing: border-box;
  text-align: left;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  width: 11rem;
  transition: all 0.2s ease;
}
.tarjeta-carta:hover{
    box-shadow: 0 8px 8px rgba(0, 0, 0, 0.6);
    transform: scale(1.02);
}

.tarjeta-carta.común {
  border-color: #2374ff;
  background: #53a2f2;
}

.tarjeta-carta.rara {
  border-color: #ffff00;
  background: #d09cf3;
}

.tarjeta-carta.épica {
  border-color: #e753d3;
  background: #75f1a5;
}

.top-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.emoji {
  font-size: 1.8rem;
}

.coste {
  font-weight: bold;
  font-size: 0.95rem;
  background: #dbeafe;
  color: #1e40af;
  padding: 4px 10px;
  border-radius: 12px;
}

.cuerpo {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.nombre {
  margin: 0;
  font-size: 1.1rem;
  font-weight: 700;
  color: #111827;
}

.habilidad {
  margin: 0;
  font-size: 0.8rem;
  color: #4b5563;
  font-style: italic;
}

.tags {
  display: flex;
  gap: 6px;
}

.tag {
  font-size: 0.75rem;
  padding: 3px 8px;
  border-radius: 6px;
  background: #e5e7eb;
  color: #374151;
  font-weight: 500;
}

.btn-add {
  width: 100%;
  padding: 8px;
  background: #10b981;
  color: white;
  border: none;
  border-radius: 6px;
  font-weight: 600;
  font-size: 0.85rem;
  cursor: pointer;
  transition: all  0.2s ease;
}

.btn-add:hover {
  filter: brightness(1.02);
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.5);
}
</style>