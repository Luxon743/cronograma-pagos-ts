<script setup lang="ts">
    import { computed, ref } from 'vue';
    import ListOfDays from "./components/ListOfDays.vue";
    import DNIInput from "./components/DNIInput.vue";

    type DiaLaboral = 'Lunes' | 'Martes' | 'Miercoles' | 'Jueves' | 'Viernes';

    const dias: DiaLaboral[] = ['Lunes', 'Martes', 'Miercoles', 'Jueves', 'Viernes'];

    const diaSeleccionado = ref<DiaLaboral>('Lunes');
    
    const dniInput = ref<string>('');

    const seleccionarDia = (dia: DiaLaboral): void =>{
        diaSeleccionado.value = dia;
    }

    const cronograma: Record<DiaLaboral, string[]> = {
        'Lunes': ['0', '1'],
        'Martes': ['2', '3'],
        'Miercoles': ['4', '5'],
        'Jueves':   ['6', '7'],
        'Viernes': ['8','9']
    }

    const correspondeCobro = computed(() =>{
        if (dniInput.value.length === 0 ) return null

        const ultimoDigito = dniInput.value.slice(-1)
        const digitosDelDia =cronograma[diaSeleccionado.value]

        return digitosDelDia.includes(ultimoDigito)
    })
</script>

<template>
    <div class="min-h-screen bg-slate-50 p-8 flex flex-col items-center">
        <h1 class="text-3xl font-extrabond text-slate-800 mb-8">Gestor de Pagos</h1>
        
        <!-- Bloque de dias moduralizado-->
        <ListOfDays/>

        <!-- Bloque del dni-->
        <DNIInput/>

        <div v-if="dniInput" class="mt-6">
            <p v-if="correspondeCobro" class="text-green-600 font-bold text-lg">¡Hoy te corresponde el pago!</p>
            <p v-else class="text-red-500">Hoy no es tu turno de cobro</p>
        </div>
    </div>
    
</template>

<style scoped></style>
