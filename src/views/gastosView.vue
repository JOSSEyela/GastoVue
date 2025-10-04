<template>
    <div class="min-h-screen flex items-center justify-center bg-gradient-to-b from-white to-sky-900">
        <div class="bg-white shadow-lg rounded-2xl p-6 w-[400px]">
        <h2 class="text-2xl font-bold mb-4 text-center text-sky-800">Mis Gastos</h2>

        <!-- Formulario -->
        <div class="flex gap-2 mb-4 ">
            <input v-model="nuevoNombre" placeholder="Nombre"
                class="border rounded p-2 w-1/2 text-gray-700" />
            <input v-model.number="nuevoMonto" type="number" placeholder="Monto"
                class="border rounded p-2 w-1/3 text-gray-700" />
            <button @click="agregarGasto"
                    class="bg-sky-600 text-white px-3 rounded hover:bg-sky-800">
            +
            </button>
        </div>

        <!-- Lista -->
        <ul class="space-y-2">
            <li v-for="(gasto, i) in gastos" :key="i"
                class="flex justify-between items-center bg-sky-100 p-2 rounded">
            <span>{{ gasto.nombre }} - ${{ gasto.monto }}</span>
            <button @click="eliminarGasto(i)" class="text-red-500">X</button>
            </li>
        </ul>

        <!-- Total -->
        <div class="mt-4 font-semibold text-lg text-center text-gray-500">
            Total: ${{ total }}
        </div>
        </div>
    </div>
    </template>

    <script setup>
    import { computed, ref } from 'vue'

    const gastos = ref([])
    const nuevoNombre = ref('')
    const nuevoMonto = ref(0)

    const agregarGasto = () => {
    if (nuevoNombre.value && nuevoMonto.value > 0) {
        gastos.value.push({ nombre: nuevoNombre.value, monto: nuevoMonto.value })
        nuevoNombre.value = ''
        nuevoMonto.value = 0
    }
    }

    const eliminarGasto = (index) => gastos.value.splice(index, 1)

    const total = computed(() =>
    gastos.value.reduce((acc, g) => acc + g.monto, 0)
    )
</script>
