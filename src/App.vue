<script setup>
import { ref } from 'vue';
import Catalogo from './components/Catalogo.vue';

const cartas = ref([
  { id: 1, nombre: "Meshuggah", habilidad: "Bleed", emoji: "🥁", tipo: "Criatura", coste: 9, rareza: "Épica" },
  { id: 2, nombre: "Muse", habilidad: "Knights of Cydonia", emoji: "🚀", tipo: "Criatura", coste: 7, rareza: "Épica" },
  { id: 3, nombre: "And One", habilidad: "Military Fashion Show", emoji: "🎹", tipo: "Criatura", coste: 4, rareza: "Rara" },
  { id: 4, nombre: "Lucybell", habilidad: "Mata El Amor", emoji: "🎸", tipo: "Criatura", coste: 5, rareza: "Rara" },
  { id: 5, nombre: "Nitzer Ebb", habilidad: "Join in the Chant", emoji: "⚡", tipo: "Hechizo", coste: 3, rareza: "Común" },
  { id: 6, nombre: "Death Grips", habilidad: "Guillotine", emoji: "🔊", tipo: "Trampa", coste: 6, rareza: "Épica" },
  { id: 7, nombre: "Blank Banshee", habilidad: "Meteor Blade", emoji: "☄", tipo: "Hechizo", coste: 2, rareza: "Rara" },
  { id: 8, nombre: "Oneohtrix Point Never", habilidad: "Replica", emoji: "🌌", tipo: "Hechizo", coste: 8, rareza: "Épica" },
  { id: 9, nombre: "Underscores", habilidad: "Spoiled Little Brat", emoji: "🎧", tipo: "Criatura", coste: 3, rareza: "Común" },
  { id: 10, nombre: "Ninajirachi", habilidad: "Start Small", emoji: "🔮", tipo: "Criatura", coste: 4, rareza: "Rara" },
  { id: 11, nombre: "Gorillaz", habilidad: "Feel Good Inc.", emoji: "🦍", tipo: "Hechizo", coste: 5, rareza: "Épica" },
  { id: 12, nombre: "Daft Punk", habilidad: "Around the World", emoji: "🤖", tipo: "Trampa", coste: 4, rareza: "Rara" },
  { id: 13, nombre: "Deftones", habilidad: "Change", emoji: "🌊", tipo: "Criatura", coste: 6, rareza: "Rara" },
  { id: 14, nombre: "Aphex Twin", habilidad: "Windowlicker", emoji: "🌀", tipo: "Hechizo", coste: 7, rareza: "Épica" },
  { id: 15, nombre: "Boards of Canada", habilidad: "Dayvan Cowboy", emoji: "📼", tipo: "Trampa", coste: 1, rareza: "Común" }
]);
</script>

<template>
  <Catalogo :cartas="cartas" />
</template>

<style>
</style>