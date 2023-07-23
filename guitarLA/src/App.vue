<script setup>
    /*SE CREAN AQUI TODO LOS REF*/
    import {ref, reactive} from 'vue'
    import {db} from './data/guitarras'
    import Guitarra from './components/Guitarra.vue'
    import Header from './components/Header.vue'
    import Footer from './components/Footer.vue'
    
    /*Aqui esta la referencia del objeto que se le esta dando*/
    /*Estamos obteniendo la api , pero no es necesario tener todo lso datos sabemos que db es un arreglo lleno de objetos
    asi que no es tan necesario definir aquello*/
    const guitarras=ref(db);

    /*Aqui creamos uno para el carrito de compras*/
    const carrito=ref([]);
    /*########SE CREA FUNCION#######*/
    /*Recordar que guitarra.cantidad es parte del objeto del prop que hemos definidos*/
    const guardarCarrito= (guitarra)=>{
        guitarra.cantidad=1; /*Se le añade los valores o un atributo más al objeto*/
        carrito.value.push(guitarra);
        console.log(carrito)
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
