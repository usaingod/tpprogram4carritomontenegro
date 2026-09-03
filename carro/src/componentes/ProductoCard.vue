<script setup>
defineProps({
  producto: Object
})

const emit = defineEmits(['agregar'])
</script>

<template>
  <div class="producto">
    <h3>{{ producto.nombre }}</h3>

    <p>Precio: ${{ producto.precio }}</p>

    <p>Stock: {{ producto.stock }}</p>

    <button
      @click="emit('agregar', producto)"
      :disabled="producto.stock === 0"
    >
      Agregar al carrito
    </button>
  </div>
</template>

<style scoped>
.producto {
  background: white;
  border: 1px solid #ccc;
  padding: 15px;
  width: 200px;
}

button {
  padding: 8px;
  cursor: pointer;
}

button:disabled {
  cursor: not-allowed;
}
</style>