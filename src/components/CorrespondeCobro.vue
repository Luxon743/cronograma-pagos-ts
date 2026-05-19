<script setup lang="ts">
    interface Props {
        dniInput: string,
        correspondeCobro: boolean | null,
    }

    const props = defineProps<Props>();
</script>

<template>
    <div v-if="dniInput" class="mt-6">
            <p v-if="correspondeCobro" class="text-green-600 font-bold text-lg">¡Hoy te corresponde el pago!</p>
            <p v-else class="text-red-500">Hoy no es tu turno de cobro</p>
    </div>
</template>

<style scoped>

</style>