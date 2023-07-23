<script setup>
    import {ref, reactive} from 'vue'
    import {db} from './data/guitarras'
    import Guitarra from './components/Guitarra.vue'
    import Header from './components/Header.vue'
    import Footer from './components/Footer.vue'
    
    const guitarras=ref(db);
    const carrito=ref([]);
    console.log(guitarras.value);
    const guardarCarrito= (guitarra)=>{
        guitarra.cantidad=1;
        carrito.value.push(guitarra);
    }
</script>

<template>
    <Header :carrito="carrito">
        
    </Header>


    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <!-- AQUI ESTA LA PARTE DE GUITARRA -->
            <Guitarra v-for="guitarra in guitarras" 
            v-bind:guitarra="guitarra"
            @guardar-carrito="guardarCarrito">
            
            </Guitarra>
        </div>
    </main>


    <Footer></Footer>
  
</template>

<style scoped>
  
</style>
