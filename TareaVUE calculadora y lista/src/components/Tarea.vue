<template>
    <div>
        <!-- Ejercicio 1 -->
        <section style="margin-bottom: 40px;">
            <h2>Calculadora de Descuento</h2>
            <label>Precio original: </label>
            <input type="number" v-model.number="precio" />
            <br />
            <label>Descuento (%): </label>
            <input type="number" v-model.number="descuento" />
            <br />
            <p>Precio final: {{ precioFinal }}</p>
        </section>

        <hr />

        <!-- Ejercicio 2 -->
        <section style="margin-top: 40px;">
            <h2>Lista de Tareas Completadas</h2>
            <ul>
            <li v-for="(tarea, index) in tareasCompletadas" :key="index">
                {{ tarea.texto }}
            </li>
            </ul>
        </section>
        </div>
    </template>

<script setup>
    import { ref, computed } from 'vue'
    
    // Ejercicio 1
    const precio = ref(0)
    const descuento = ref(0)
    
    const precioFinal = computed(() => {
        return precio.value - (precio.value * descuento.value / 100)
    })
    
    // Ejercicio 2
    const tareas = ref([
        { texto: 'comprar juegos', completada: true },
        { texto: 'comer', completada: false },
        { texto: 'Dormir', completada: true },
        { texto: 'Jugar videojuegos', completada: false },
    ])
    
    const tareasCompletadas = computed(() => {
        return tareas.value.filter(t => t.completada)
    })
</script>
