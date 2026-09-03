<script setup>
import { computed } from 'vue'

const props = defineProps({
  carrito: Array
})

const emit = defineEmits(['eliminar'])

const total = computed(() => {
  return props.carrito.reduce((suma, producto) => {
    return suma + producto.precio
  }, 0)
})
</script>

<template>
  <div>
    <h2>Carrito</h2>

    <p v-if="carrito.length === 0">
      El carrito está vacío
    </p>

    <div v-for="(producto, index) in carrito" :key="index">
      <p>
        {{ producto.nombre }} - ${{ producto.precio }}
        <button @click="emit('eliminar', producto)">
          Eliminar
        </button>
      </p>
    </div>

    <h3>Total: ${{ total }}</h3>
  </div>
</template>