<script setup lang="ts">
    type DiaLaboral = 'Lunes' | 'Martes' | 'Miercoles' | 'Jueves' | 'Viernes';

    const dias: DiaLaboral[] = ['Lunes' | 'Martes' | 'Miercoles' | 'Jueves' | 'Viernes'];

    const diaSeleccionado = ref<DiaLaboral>('Lunes');

    const seleccionarDia = (dia: DiaLaboral): void =>{
        diaSeleccionado.value = dia;
    }
</script>

<template>
  <h1>You did it!</h1>
  <p>
    Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
    documentation
  </p>
</template>

<style scoped></style>
