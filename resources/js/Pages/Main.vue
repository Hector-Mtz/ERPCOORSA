<script setup >
import AppLayout from '@/Layouts/AppLayout.vue';
import { Inertia } from '@inertiajs/inertia'
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';
import { onMounted, reactive, ref, watch } from 'vue';
import axios from 'axios';
import ModuleCliente from '@/Components/clientes.vue';

var props = defineProps({
    clientes:Object,
    cecos: Object
});
</script>

<template>
    
    <AppLayout title="Presupuestos">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Presupuestos
            </h2>
        </template>
 
        <div class="py-12 fondo_general" >
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <ModuleCliente :clientes = clientes :cecos = cecos></ModuleCliente> <!--Modulo amcharts-->
                </div>
            </div>
        </div>
    </AppLayout>
</template>
