<script setup>
import { ref, onMounted, onUnmounted, useTemplateRef, watch, nextTick } from 'vue'
import TarjetaProducto from './TarjetaProducto.vue'

const props = defineProps({
    productos: {
        type: Array,
        required: true
    }
})

const cargando = ref(true)
let timer = null

const box = useTemplateRef('box')

function esperar(ms) {
    return new Promise(resolve => setTimeout(resolve, ms))
}


async function cargarProductos() {
    if (cargando.value) {
        await esperar(1000)
        cargando.value = false
    }
}

onMounted(() => {
    cargarProductos()
    timer = setInterval(() => {
        console.log('polling ejecutándose: recargando productos ...')
        cargarProductos()
    }, 3000)
})

watch(() => props.productos.length, async (nuevoTamano, viejoTamano) => {
    if (nuevoTamano > viejoTamano) {
        await nextTick() 
        if (box.value) {
            box.value.scrollTo({
                top: box.value.scrollHeight,
                behavior: 'smooth' 
            })
        }
    }
})


onUnmounted(() => {
    clearInterval(timer)
    console.log('ListaProductos desmontado - polling detenido')
})
</script>

<template>
    <div v-if="cargando" class="loading">
        <p>Cargando...</p>
    </div>

    <div v-else ref="box" class="lista-contenedor">
        <TarjetaProducto v-for="prod in productos" :key="prod.id">
            <template #header>
                <h3>{{ prod.nombre }}</h3>
                <small class="tag">{{ prod.categoria }}</small>
            </template>

            <template #body="{ expandida, toggleExpandir }">
                <button @click="toggleExpandir" class="btn-toggle">
                    {{ expandida ? 'Ocultar info' : 'Ver precio y stock' }}
                </button>
                <div v-if="expandida" class="detalle">
                    <p><strong>Precio:</strong> ${{ prod.precio.toLocaleString() }}</p>
                    <p><strong>Stock disponible:</strong> {{ prod.stock }} unidades</p>
                </div>
            </template>

            <template #footer>
                <button class="btn-comprar" :disabled="prod.stock === 0">Comprar</button>
            </template>
        </TarjetaProducto>
    </div>
</template>

<style scoped>
.lista-contenedor {
    max-height: 300px;
    overflow-y: auto;
    border: 1px solid #ccc;
    padding: 10px;
}
</style>