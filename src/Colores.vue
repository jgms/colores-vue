<template>
    <Formulario @crear="crearColor" />
    <ul>
        <Item @borrar="borrarColor" v-for="{id,r,g,b} in colores" :id="id" :r="r" :g="g" :b="b" />
    </ul>
</template>

<script setup>
    import { ref, onMounted } from "vue"
    import Formulario from "./Formulario.vue"
    import Item from "./Item.vue"

    const colores = ref([])

    onMounted( () => {
        fetch("https://api-ejemplo-0mcf.onrender.com/colores")
        .then(respuesta => respuesta.json())
        .then(respuesta => {
            colores.value = respuesta
        })

    })

    function crearColor(color){
        colores.value.push(color)
    }

    function borrarColor(id){
        colores.value = colores.value.filter( color => color.id != id )
    }


</script>