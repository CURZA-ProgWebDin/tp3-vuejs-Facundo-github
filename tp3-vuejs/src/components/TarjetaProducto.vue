<script setup>
import { ref } from 'vue'

const expandida = ref(false)

const toggleExpandir = () => {
    expandida.value = !expandida.value
}
</script>

<template>
    <div class="tarjeta-producto">
        <header class="tarjeta-header">
            <slot name="header"></slot>
        </header>

    <main class="tarjeta-body">
        <slot name="body" :expandida="expandida" :toggleExpandir="toggleExpandir" ></slot>
    </main>

    <footer class="tarjeta-footer">
        <slot name="footer">
            <span class="fallback-text">Sin acciones disponibles</span>
        </slot>
    </footer>

    </div>
</template>

<style scoped>
.tarjeta-producto {
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 16px;
    margin-bottom: 12px;
    background-color: #fff;
    box-shadow: 0 2px 4 px rgb(0,0,0,0.05);
}
.tarjeta-header {
    font-weight: bold;
    border-bottom: 1px solid #eee;
    padding-bottom: 8px;
}
.tarjeta-body {
    padding: 12px 0;
}
.tarjeta-footer {
    border-top: 1px solid #eee;
    padding-top: 8px;
    text-align: right;
}
.fallback-text {
    color: #888;
    font-style: italic;
}

</style>