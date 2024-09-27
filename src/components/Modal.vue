<script setup>
    import { ref } from 'vue';
    import Alerta from './Alerta.vue';

    import cerrarModal from '../assets/img/cerrar.svg'

    const emit = defineEmits(['ocultar-modal', 'update:nombre', 'update:cantidad', 'update:categoria', 'guardar-gasto'])

    const props = defineProps({
        modal:{
            type: Object,
            required: true
        },
        nombre:{
            type: String,
            required: true
        },
        cantidad:{
            type: [String, Number],
            required: true
        },
        categoria:{
            type: String,
            required: true
        }
    })

    const error = ref('')

    const agregarGasto = () => {
        const { nombre,cantidad,categoria } = props;

        if([nombre,cantidad,categoria].includes('')){
            error.value = 'Los campos son obligatorios'
            console.log('hay campos vacios')
            setTimeout(() =>{
                error.value = ''
            },2500)
            return
        }

        if(cantidad <= 0){
            error.value = 'No es una cantidad válida'
            setTimeout(() =>{
                error.value = ''
            },2500)
            return
        }

        emit('guardar-gasto')
        console.log('emitiendo gasto')
    }
</script>

<template>
    <div class="modal">
        <div class="cerrar-modal">
            <img
                :src="cerrarModal"
                @click="$emit('ocultar-modal')"
            />
        </div>
        <div
            class="contenedor contenedor-formulario"
            :class="[modal.animar ? 'animar' : 'cerrar']"
            >
            
            <form
                class="nuevo-gasto"
                @submit.prevent="agregarGasto"
                >
                <legend>Añadir gasto</legend>
                <Alerta v-if="error">
                    <p>{{ error }}</p>
                </Alerta>
                <div class="campo">
                    <label for="nombre">Nombre gasto:</label>
                    <input
                        type="text"
                        id="nombre"
                        placeholder="Añade el nombre del gasto"
                        :value="nombre"
                        @input="$emit('update:nombre', $event.target.value)"
                    />
                </div>
                <div class="campo">
                    <label for="cantidad">Cantidad:</label>
                    <input
                        type="number"
                        id="cantidad"
                        placeholder="Añade la cantidad del gasto"
                        min="0"
                        :value="cantidad"
                        @input="$emit('update:cantidad', +$event.target.value)"
                    />
                </div>
                <div class="campo">
                    <label for="categoria">Categoría:</label>
                    <select name=""
                        id="categoria"
                        :value="categoria"
                        @input="$emit('update:categoria', $event.target.value)"
                        >
                        <option value="">-- Seleccione --</option>
                        <option value="ahorro">Ahorro</option>
                        <option value="comida">Comida</option>
                        <option value="casa">Casa</option>
                        <option value="varios">Varios</option>
                        <option value="ocio">Ocio</option>
                        <option value="salud">Salud</option>
                        <option value="suscripciones">Suscripciones</option>
                    </select>
                </div>
                <input
                    type="submit"
                    value="Añadir gasto"                    
                />
            </form>
        </div>
    </div>
</template>



<style>
    .modal{
        position: absolute;
        background-color: rgb(0 0 0 / 0.9);
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
    }

    .contenedor-formulario{
        transition: all 0.3s ease-in;
        opacity: 0;

        &.animar{
            opacity: 1;
        }

        &.cerrar{
            opacity: 0;
        }
    }

    .cerrar-modal{
        position: absolute;
        right: 3rem;
        top: 3rem;
        cursor: pointer;
        img{
            width: 3rem;
        }
    }

    .nuevo-gasto{
        margin: 10rem auto 0 auto;
        display: grid;
        gap: 2rem;

        input,select{
            background-color: var(--gris-claro);
            border-radius: 1rem;
            padding: 1rem;
            border: none;
            font-size: 2.2rem;
        }

        label{
            color: var(--blanco);
            font-size: 3rem;
        }

        input[type="submit"]{
            background-color: var(--azul);
            color: var(--blanco);
            font-weight: 700;
            cursor: pointer;
        }

        legend{
            text-align: center;
            color: var(--blanco);
            font-size: 3rem;
            font-weight: 700;
        }
    }

    .campo{
        display: grid;
        gap: 2rem;
    }

</style>