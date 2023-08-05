<script setup>
    import { ref, reactive } from 'vue';
    import Alert from './alert.vue';
    const nombre = ref('Cali');

    // Otra forma de leer con un method handler

    const alerta = reactive({

    });

    const leer = (e) => {
        nombre.value = e.target.value;
    }

    const registro = reactive({
        nombre:'',
        propietario:'',
        email: '',
        fecha: '',
        sintomas: ''
    });

    const validar = e => {
        //e.preventDefault(); //Para detener que se ejecute el evento de hacer refersh al dar submit

        //[registro.nombre, paciente.propietario].includes('') -> Es para checar si tiene algun espacio
        if(Object.values(registro).includes('')){
            alerta.mensaje = 'Todos los campos son obligatorios';
            alerta.tipo ='error';
            return;
        }else{
            alerta.mensaje = 'Guardado Correctamente';
            alerta.tipo = 'exito';
            return;
        }
    }
</script>


<template>
    <!-- va a agarrar una de dos columnas -->
    <div class="md:w-1/2"> 
        <h1 class="font-balck text-3xl text-center">Seguimiento de Pacientes</h1>
        <p class="text-lg mt-5 text-center mb-10">
            Anadir Paciente
            <span class="text-indigo-600 font-bold">Adminstralos</span>
        </p>

        <Alert v-if="alerta.mensaje" :alerta="alerta"></Alert>


        <!-- Crear el formularlo el shadow sirve para poner somreba y rounded para agregar border radius -->
        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" v-on:submit.prevent="validar">
            <!-- En se puede usar v-model en vez de: :value = "nombre" @input="(e) => nombre = e.target.value" -->
            <div class="mb-5">
                <label for="nombre" class="block text-gray-700 uppercase font-bold"> Nombre de la mascota </label>
                <input type="text" id="nombre" placeholder="Nombre" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="registro.nombre">
            </div> 

            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold"> Propietario de la Mascota </label>
                <input type="text" id="propietario" placeholder="Propietario" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="registro.propietario">
            </div> 

            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold"> Email del Propietario </label>
                <input type="email" id="email" placeholder="Email" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="registro.email">
            </div> 

            <div class="mb-5">
                <label for="date" class="block text-gray-700 uppercase font-bold"> Fecha</label>
                <input type="date" id="date"  class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="registro.fecha">
            </div> 

            <div class="mb-5">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold"> Sintomas de la Mascota</label>
                <textarea id="sintomas" placeholder="Email" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40" v-model="registro.sintomas"></textarea>
            </div> 

            <input type="submit" class="bg-indigo-600 p-3 w-full text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors" value="Registrar">  

        </form>
    </div>
</template>