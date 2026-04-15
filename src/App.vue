<script setup>
import {ref,reactive, onMounted} from "vue";
import {db} from './data/guitarras';
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import GuitarraCard from "./components/GuitarraCard.vue";

// const state = reactive({
//     guitarass:db
// })

// console.log(state);

const guitarras = ref(db);
const carritos = ref([])

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
    console.log("Componente montado");
})

const incrementarCantidad = ()=>{
    console.log("Incrementar....")
}

const decrementarCantidad = ()=>{
    console.log("decrementar...")
}

</script>

<template>
    <Header  
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
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

