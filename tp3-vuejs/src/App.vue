<script setup>
import TarjetaProducto from './components/TarjetaProducto.vue'
import PanelPestanas from './PanelPestanas.vue'
</script>

<template>
  <main class="app-main">
    <h1>TP3 - CICLO DE VIDA, COMPONENTES DINÁMICOS Y SLOTS</h1>

    <section class="pruebas-slots">
      <h2>Prueba de Slots (Parte 1)</h2>
      <div class="grid-tarjetas">
        <TarjetaProducto>
          <template #header>
            <h3>Instancia 1: Completa</h3>
            <span class="badge">Test A</span>
          </template>

          <template #body="{ expandida, toggleExpandir }">
            <p>Controlador de estado</p>
            <button @click="toggleExpandir" class="btn-demo">
              {{ expandida ? 'cerrar' : 'Expandir' }}
            </button>
          </template>

          <template #footer>
            <button class="btn-success">Accion Aprobada</button>
          </template>

        </TarjetaProducto>

        <TarjetaProducto>
          <template #header>
            <h3>Instancia 2: Sin Footer</h3>
            <span class="badge">Test B</span>
          </template>

          <template #body="{ expandida, toggleExpandir }">
            <p>Al no definir el bloque template footer en el padre, se renderiza automaticamente el fallback definido en el hijo</p>
            <button @click="toggleExpandir" class="btn-demo">Toggle</button>
            <p v-if="expandida">Estado Actual: Expandido</p>
          </template>
        </TarjetaProducto>

        <TarjetaProducto>
          <template #header>
            <h3>Instancia 3: Variante Libre</h3>
          </template>

          <template #body>
            <p>Acá se muestra un layaout básico sin lógica de expansión</p>
          </template>

          <template #footer>
            <a href="#">Ver links alternativos</a>
          </template>
        </TarjetaProducto>

      </div>
    </section>
    <hr />

    <PanelPestanas></PanelPestanas>

  </main>
</template>

<style>
body {
  background-color: #f4f6f8;
  margin: 0;
  color: #2c3e50;
  font-family: sans-serif;
}
</style>

<style scoped>
.app-main {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}
.grid-tarjetas {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap:16px;
  margin-bottom: 30px;
}
.badge {
  background: #35495e;
  color: white;
  padding: 2px 5px;
  border-radius: 3px;
  font-size: 0.75rem;
}
.btn-demo {
  background: #eaeaea;
  border: 1px solid #ccc;
  padding: 4px 8px;
  border-radius: 4px;
  cursor: pointer;
}
.alert-info {
  color: #31708f;
  background-color: #d9edf7;
  padding: 4px;
  border-radius: 4px;
  margin-top: 5px;
  font-size: 0.9rem;
}
.btn-success {
  background: #42b883;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}
</style>
