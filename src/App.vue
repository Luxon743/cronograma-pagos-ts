<script setup lang="ts">
    import { computed, ref } from 'vue';
    import ListOfDays from "./components/ListOfDays.vue";
    import DNIInput from "./components/DNIInput.vue";
import CorrespondeCobro from './components/CorrespondeCobro.vue';

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

    const actualizarDni = (dni: string) : void=>{
        dniInput.value = dni;
    }
</script>

<template>
    <div class="min-h-screen bg-slate-50 p-8 flex flex-col items-center">
        <h1 class="text-3xl font-extrabond text-slate-800 mb-8">Gestor de Pagos</h1>
        
        <!-- Bloque de dias moduralizado-->
        <ListOfDays @nuevoDiaSeleccionado="seleccionarDia"/>

        <!-- Bloque del dni-->
        <DNIInput @nuevoDniIngresado="actualizarDni"/>

        <CorrespondeCobro
        :dniInput="dniInput"
        :correspondeCobro="correspondeCobro"
        />
    </div>
    
</template>

<style scoped></style>
