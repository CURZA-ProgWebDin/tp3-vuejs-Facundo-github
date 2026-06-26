<script setup>
import { onMounted, onUnmounted, onActivated, onDeactivated, computed } from 'vue'
import { productos } from '../../data/productos.js'
import ListaProductos from '../ListaProductos.vue'

const electronica = computed(() =>{return productos.filter(p => p.categoria === 'Electrónica')} )

onMounted(() => console.log('tabElectronica - montado') )
onUnmounted(() => console.log('tabElectronica - desmontado') )
onActivated(() => console.log('tabElectronica - activado') )
onDeactivated(() => console.log('tabElectronica - desactivado') )

</script>

<template>
    <div>
        <h2>Categoria: Electrónica</h2>
        <ListaProductos :productos="electronica" />
    </div>
</template>