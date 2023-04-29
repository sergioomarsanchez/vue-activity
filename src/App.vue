<template>
  <main class="container">
    <h2>Cena {{ contador+1 }} con el rey godo {{ rey }}</h2>
    <h3 class="Precio">Precio: {{ productos[contador].precio }} Usd</h3>
    <div v-if="productos[contador].finDeSemana" class="soloFinesDeSemana dias">(Sólo fines de Semana)</div>
    <div v-else class="todosLosDias dias">(De lunes a domingo)</div>
    <div v-show="!productos[contador].finDeSemana">
      Ahora un 10% dto:
      {{ nuevoPrecio }} Usd
      <img src="/oferta.png" alt="Oferta 10% tag" class="onSale" />
    </div>
    <img :src="reyImg" at="" />
    <button @:click="siguiente">Siguiente ({{ contador+1 }}/ {{ total }})</button>
  </main>
</template>


<script setup>
import { productos } from './datos'
import { ref, computed } from 'vue'
const  ruta = `https://www.html6.es/img/rey_`
const contador=ref(0)
const total = productos.length

const siguiente = ()=>{
  if(contador.value===productos.length-1){contador.value=0}
  else contador.value++
}
const rey = computed(()=>{
  const nombre = productos[contador.value].nombre.toLowerCase()
 
  return  nombre.substring(0,1).toUpperCase() + nombre.substring(1)
})
const reyImg = computed(()=>{
  const nombre = productos[contador.value].nombre.toLowerCase()
  return  ruta + nombre
})
const nuevoPrecio = computed(()=>{
  const precio = productos[contador.value].precio / 1.1
  return  precio.toFixed(2)
})
</script>

<style scoped>
.container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  max-width: 25rem;
  max-height: 35rem;
  text-align: center;
  margin: 2rem;
  background-color: rgb(194, 126, 0);
  border: solid 2px maroon;
  border-radius: 2rem;
  padding: 4rem;
}
.todosLosDias{
  background-color:green;
}
.soloFinesDeSemana{
background-color: red;
}
.dias{
display: inline-block;
  color: white;
  padding: 4px 17px;
  font-size: 0.9em;
  border-radius: 4px;
  margin: 5px 0 10px;
  width: fit-content;
  display: flex;
  align-self: center;
}
button {
  bottom: 5px;
  border-radius: 5px;
  background-color: maroon;
  color: white;
  padding: 0.5rem;
  border: solid 1px white;
  transition: 300ms ease;
  cursor: pointer;
  width: fit-content;
  display: flex;
  align-self: center;
  margin: 2rem;
}
button:hover{
  background-color: rgb(167, 3, 3);
  box-shadow: 0 0 10px 1px black;
}
.onSale{
  width: 15px;
  height: 15px;
}
</style>
