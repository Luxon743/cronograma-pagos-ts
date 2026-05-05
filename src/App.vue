<script setup lang="ts">
    import { computed, ref } from 'vue';

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
        <div class="flex gap-2">
            <button v-for="dia in dias" :key="dia"
            :class="[
                'px-6 py-2 font-medium rounded-full transition-all duration-200',
                diaSeleccionado === dia 
                    ?'bg-indigo-600 text-white shadow-lg shadow-indigo-200'
                    :'bg-white text-indigo-600 border border-indigo-200 hover:bg-indigo-50'
            ]" @click="seleccionarDia(dia)">
                {{ dia }}
            </button>
        </div>
        <div class="w-full max-w-md bg-white p-6 rounded-2xl shadow-sm border border-slate-200 mt-6">
            <label class="block text-sm font-semibold text-slate-700 mb-2">Ingrese su DNI</label>
            <input
                v-model="dniInput"
                type="text"
                placeholder="Ej: 40123456"
                maxlength="8"
                class="w-full p-3 border border-slate-300 rounded-xl foucs:ring-2 focus:ring-indigo-500 outline-none transition-all"
            />
        </div>
        <div v-if="dniInput" class="mt-6">
            <p v-if="correspondeCobro" class="text-green-600 font-bold text-lg">¡Hoy te corresponde el pago!</p>
            <p v-else class="text-red-500">Hoy no es tu turno de cobro</p>
        </div>
    </div>
    
</template>

<style scoped></style>
