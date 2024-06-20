<script setup>
    import { reactive, ref } from "vue";
    import Alerta from "./Alerta.vue";

    const búsqueda = reactive({
        ciudad: '',
        país: ''
    });
    const países = [
        { código: 'US', nombre: 'Estados Unidos' },
        { código: 'MX', nombre: 'México' },
        { código: 'AR', nombre: 'Argentina' },
        { código: 'CO', nombre: 'Colombia' },
        { código: 'CR', nombre: 'Costa Rica' },
        { código: 'ES', nombre: 'España' },
        { código: 'PE', nombre: 'Perú' },
        { código: 'VE', nombre: 'Venezuela' }
    ]
    const error = ref('');
    const emit = defineEmits(['obtener-Clima']);
    const consultarClima = () => {
        if(Object.values(búsqueda).includes('')){
            error.value = 'Todos los campos son obligatorios';
            return
        }
        error.value='';
        emit('obtener-Clima', búsqueda);
    };
    
</script>

<template>
    <form 
        class="formulario"
        @submit.prevent="consultarClima"
    >
        <Alerta v-if="error">{{ error }}</Alerta>
        <div class="campo">
            <label for="ciudad">Ciudad</label>
            <input type="text" id="ciudad" placeholder="Ciudad" v-model="búsqueda.ciudad">
        </div>
        <div class="campo">
            <label for="país">País</label>
            <select id="país" v-model="búsqueda.país">
                <option value="">-- Seleccione un País--</option>
                <option v-for="país in países" :value="país.código">{{ país.nombre }}</option>
            </select>
        </div>
        <input type="submit" value="Consultar Clima">
    </form>
</template>