<script setup>
    import cerrarModal from '../assets/img/cerrar.svg'

    const emit = defineEmits(['ocultar-modal'])

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
            <form class="nuevo-gasto">
                <legend>Añadir gasto</legend>
                <div class="campo">
                    <label for="nombre">Nombre gasto:</label>
                    <input
                        type="text"
                        id="nombre"
                        placeholder="Añade el nombre del gasto"
                        :value="nombre"
                    />
                </div>
                <div class="campo">
                    <label for="cantidad">Cantidad:</label>
                    <input
                        type="number"
                        id="cantidad"
                        placeholder="Añade la cantidad del gasto"
                        :value="cantidad"
                    />
                </div>
                <div class="campo">
                    <label for="categoria">Categoría:</label>
                    <select name=""
                        id="categoria"
                        :value="categoria"
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