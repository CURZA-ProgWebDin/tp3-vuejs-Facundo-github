<script setup>
import { onMounted, onUnmounted, onActivated, onDeactivated, computed } from 'vue'
import { productos } from '../../data/productos.js'
import ListaProductos from '../ListaProductos.vue'

const perifericos = computed(() => {
    return productos.filter(p => p.categoria === 'Periféricos')
} )

onMounted(() => console.log('TabPerifericos - montado'))
onUnmounted(() => console.log('TabPerifericos - desmontado') )
onActivated(() => console.log('TabPerifericos - activado') )
onDeactivated(() => console.log('TabPerifericos - desactivado') )

</script>

<template>
    <div>
        <h2>Categoría: Periféricos</h2>
        <ListaProductos :productos="perifericos" />
    </div>
</template>

<style scoped>
</style>