<script setup>
import { ref } from 'vue';

// ejercicio 1
const tareas = ref([
    'Jugar en la pc',
    'Ver anime', 
    'Leer manga'
]);

const completadas = ref(Array(tareas.value.length).fill(false));
const funcaTarea = (index) => {
    completadas.value[index] = !completadas.value[index];
};

// ejercicio 2
const fechaNacimiento = ref('');
const edad = ref(0);

const calcularEdad = () => {
    const hoy = new Date();
    const fechaNac = new Date(fechaNacimiento.value);
    
    if (fechaNac > hoy) {
        edad.value = -1;
        return;
    }
    
    let edadCalculada = hoy.getFullYear() - fechaNac.getFullYear();
    const mes = hoy.getMonth() - fechaNac.getMonth();
    
    if (mes < 0 || (mes === 0 && hoy.getDate() < fechaNac.getDate())) {
        edadCalculada--;
    }
    
    edad.value = edadCalculada;
};
</script>

<template>
    <div>
        <h3>ejer 1</h3>
        <div v-for="(tarea, index) in tareas" :key="index">
            <input 
                type="checkbox"
                :checked="completadas[index]"
                @change="funcaTarea(index)"
            />
            <span :class="{ 'tarea-completada': completadas[index] }">
                {{ tarea }}
            </span>
            <span>{{ completadas[index] ? ' - Completada' : ' - Pendiente' }}</span>
        </div>
    </div>

    <div>
        <h3>ejer 2</h3>
        <form @submit.prevent="calcularEdad">
            <label for="fechaNacimiento">Ingresa tu fecha de nacimiento:</label>
            <input 
                type="date" 
                id="fechaNacimiento"
                v-model="fechaNacimiento" 
                required
            >
            <button type="submit">Calcular</button>
        </form>
        
        <div v-if="edad !== 0">
            <p v-if="edad > 0 && edad >= 18">Eres mayor de edad</p>
            <p v-else-if="edad > 0 && edad < 18">Eres menor de edad</p>
            <p v-else>¡La fecha ingresada es en el futuro!</p>
        </div>
    </div>
</template>
