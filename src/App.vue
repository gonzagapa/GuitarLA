<script setup>
import {ref,reactive, onMounted} from "vue";
import {db} from './data/guitarras';
import Header from "./components/Header.vue";
import GuitarraCard from "./components/GuitarraCard.vue";

// const state = reactive({
//     guitarass:db
// })

// console.log(state);

const guitarras = ref(db);

onMounted(()=>{
    console.log("Componente montado");
})

</script>

<template>
    <Header/>
    <!-- MAIN CONTENT -->
      <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">

            <GuitarraCard v-for="guitarra in guitarras" :guitarra="guitarra" />

        </div>
    </main>
</template>

<style scoped>

</style>
