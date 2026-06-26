<script setup>
import { shallowRef } from 'vue'
import TabTodos from './components/tabs/TabTodos.vue'
import TabElectronica from './components/tabs/TabElectronica.vue'
import TabPerifericos from './components/tabs/TabPerifericos.vue'

const tabActivoNormal = shallowRef(TabTodos)
const tabActivoKeepAlive = shallowRef(TabTodos)
</script>

<template>
    <div class="panel-container">

        <section class="demo-section">
            <h3>Version Sin KeepAlive</h3>
            <div class="tabs-buttons">
                <button @click="tabActivoNormal= TabTodos" :class="{ active: tabActivoNormal === TabTodos }">Todos</button>                
                <button @click="tabActivoNormal= TabElectronica" :class="{ active: tabActivoNormal === TabElectronica }">Electrónica</button>
                <button @click="tabActivoNormal= TabPerifericos" :class="{ active: tabActivoNormal === TabPerifericos }">Periféricos</button>
            </div>

            <div class="tab-content">
                <component :is="tabActivoNormal" />
            </div>
        </section>

        <hr class="divider" />

        <section class="demo-section">
            <h3>Versión con KeppAlive</h3>
            <div class="tabs-buttons">
                <button @click="tabActivoKeepAlive = TabTodos" :class="{ active: tabActivoKeepAlive === TabTodos}">Todos</button>
                <button @click="tabActivoKeepAlive = TabElectronica" :class="{ active: tabActivoKeepAlive === TabElectronica}">Electrónica</button>
                <button @click="tabActivoKeepAlive = TabPerifericos" :class="{ active: tabActivoKeepAlive === TabPerifericos}">Periféricos</button>
            </div>
            
            <div class="tab-content border-keepalive">
                <keep-alive>
                    <component :is="tabActivoKeepAlive"></component>
                </keep-alive>
            </div>

        </section>
    </div>
</template>

<style scoped>
.panel-container {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-top: 20px;
}

.demo-section {
    background: #fff;
    padding: 16px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    border: 1px solid #eee;
}

.demo-section h3 {
    margin-top: 0;
    margin-bottom: 12px;
    color: #2c3e50;
    font-size: 1.1rem;
}

.tab-buttons {
    display: flex;
    gap: 8px;
    margin-bottom: 12px;
    border-bottom: 2px solid #eaeaea;
    padding-bottom: 8px;
}

.tab-buttons button {
    background: #eaeaea;
    color: #2c3e50;
    border: 1px solid#ccc;
    padding: 6px 12px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
    transition: all 0.2s ease;
}

.tab-buttons button:hover {
    background: #ddd;
}

.tab-buttons button.active {
    background: #42b883;
    color:white;
    border-color: #42b883;
}

.tab-content {
    padding: 12px 0;
}

.border-keepalive {
    border-left: 4px solid #35495e;
    padding-left: 12px;
}

.divider {
    border: 0;
    height: 1px;
    background: #ccc;
    margin: 10px 0;
}

</style>