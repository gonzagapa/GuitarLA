<script setup>
import {ref, onMounted} from "vue";
import {db} from './data/guitarras';
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import GuitarraCard from "./components/GuitarraCard.vue";


const guitarras = ref([]);
const carritos = ref([])
const guitarraHighlighted = ref({})

const agregarCarrito = (guitarra)=>{

    let existeGuitarra = carritos.value.find( item => item.id === guitarra.id);
    if(existeGuitarra){

        existeGuitarra.cantidad += 1;
        return;
    }

    guitarra.cantidad = 1;
    carritos.value.push(guitarra)
}

onMounted(()=>{
    guitarras.value = db;
    guitarraHighlighted.value = db[3];
})

const incrementarCantidad = (id)=>{
    const guitarra = carritos.value.find(item => item.id === id);
    guitarra.cantidad++
}

const decrementarCantidad = (id)=>{
    const guitarra = carritos.value.find(item => item.id === id);
    if(guitarra.cantidad > 0){
        guitarra.cantidad -=1
    }
}

const eliminarElemento = (id)=>{
    carritos.value = carritos.value.filter((item => item.id !== id))
}

const vaciarCarrito = ()=>{
    carritos.value = []
}

</script>

<template>
    <Header  
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
    @agregar-carrito="agregarCarrito"
    @eliminar-carrito="eliminarElemento"
    @vaciar-carrito="vaciarCarrito"
    :guitarra="guitarraHighlighted"
    :carritos="carritos"/>
    <!-- MAIN CONTENT -->
      <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">

            <GuitarraCard @agregar-carrito="agregarCarrito" v-for="guitarra in guitarras" :guitarra="guitarra" />

        </div>
    </main>

    <Footer/>
</template>

