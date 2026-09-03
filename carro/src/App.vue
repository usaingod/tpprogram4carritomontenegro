<script setup>
import { ref } from 'vue'
import ProductoCard from './componentes/ProductoCard.vue'
import Carrito from './componentes/Carrito.vue'

const productos = ref([
  { id: 1, nombre: 'Remera', precio: 15000, stock: 5 },
  { id: 2, nombre: 'Pantalón', precio: 25000, stock: 3 },
  { id: 3, nombre: 'Zapatillas', precio: 50000, stock: 2 }
])

const carrito = ref([])

function agregarAlCarrito(producto) {
  if (producto.stock > 0) {
    carrito.value.push(producto)
    producto.stock--
  }
}

function eliminarDelCarrito(producto) {
  const indice = carrito.value.findIndex(
    item => item.id === producto.id
  )

  if (indice !== -1) {
    carrito.value.splice(indice, 1)
    producto.stock++
  }
}
</script>

<template>
  <main>
    <h1>Carrito de compras</h1>

    <h2>Productos</h2>

    <div class="productos">
      <ProductoCard
        v-for="producto in productos"
        :key="producto.id"
        :producto="producto"
        @agregar="agregarAlCarrito"
      />
    </div>

    <Carrito
      :carrito="carrito"
      @eliminar="eliminarDelCarrito"
    />
  </main>
</template>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  background: #f5f5f5;
}

main {
  width: 800px;
  margin: 30px auto;
}

.productos {
  display: flex;
  gap: 15px;
}
</style>