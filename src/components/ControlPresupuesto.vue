<script setup>
    import imagen from '../assets/img/grafico.jpg';

    import { formatearCantidad } from '../helpers';

    const props = defineProps({
        presupuesto:{
            type: Number,
            required: true
        },
        disponible:{
            type: Number,
            required: true
        },
        gastado:{
            type: Number,
            required: true
        }
    })

</script>

<template>
    <div class="dos-columnas">
        <div class="contenedor-grafico">
            <img
                :src="imagen"
            />
        </div>
        <div class="contenedor-presupuesto">
            <button class="reset-app">
                Resetear app
            </button>
            <p>
                <span>Presupuesto:</span>
                {{ formatearCantidad(presupuesto) }}
            </p>
            <p>
                <span>Disponible:</span>
                {{ formatearCantidad(disponible) }}
            </p>
            <p>
                <span>Gastado:</span>
                {{ formatearCantidad(gastado) }}
            </p>
        </div>
    </div>
</template>


<style scoped>
    .dos-columnas{
        display: flex;
        flex-direction: column;
    }

    .dos-columnas > :first-child{
        margin-bottom: 3rem;
    }

    .contenedor-presupuesto{
        width: 100%;
        p{
            font-size: 2.4rem;
            text-align: center;
            color: var(--gris-oscuro);
        }
        span{
            font-weight: 900;
            color: var(--azul);
        }
    }

    .reset-app{
        background-color: #db2777;
        border: none;
        padding: 1rem;
        width: 100%;
        color: var(--blanco);
        font-weight: 900;
        text-transform: uppercase;
        border-radius: 1rem;
        transition-property: background-color;
        transition-duration: 0.3s;

        &:hover{
            cursor: pointer;
            background-color: #bb1a62;

        }
    }

    @media (width >= 768px) {
        .dos-columnas{
            flex-direction: row;
            gap: 4rem;
            align-items: center;
        }
         .dos-columnas > :first-child{
            margin-bottom: 0rem;
        }
        .contenedor-presupuesto{
            p{
                /* font-size: 2.4rem; */
                text-align: left;
            }
            span{

            }
        }
    }
    
    
</style>