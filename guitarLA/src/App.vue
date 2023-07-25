<script setup>
    /*SE CREAN AQUI TODO LOS REF*/
    import {ref, reactive, onMounted} from 'vue'
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
    const primario=ref(db[3])
    onMounted(()=>{})
    /*########SE CREA FUNCION#######*/
    /*Recordar que guitarra.cantidad es parte del objeto del prop que hemos definidos*/
    const guardarLocalStorage=()=>{
        localStorage.setItem('carrito',JSON.stringify(carrito.value))
    }
    const guardarCarrito= (guitarra)=>{
        

        const existeCarrito= carrito.value.findIndex(producto=>producto.id===guitarra.id);
        /*aqui se pone la guitarra por cada respectivo for en GUITARRAS*/
        
        if(existeCarrito>=0){
            carrito.value[existeCarrito].cantidad++
        }else{
        guitarra.cantidad=1;
        carrito.value.push(guitarra);
        }
    }
    const decrementarCantidad=(id)=>{
        /*eL VALRO QUE SE LE DA "PRODUCTO" es simple un valor o un alias noteien mucha eerelevancia o esta trayendo de otro componente*/
        const index=carrito.value.findIndex(producto=>producto.id===id)
        if(carrito.value[index].cantidad>1)
        carrito.value[index].cantidad--
    }
    const aumentarCantidad=(id)=>{
        const index=carrito.value.findIndex(producto=>producto.id===id)
        carrito.value[index].cantidad++
        console.log('AUmentando')
    }
    const eliminarProducto= (id)=>{
        carrito.value=carrito.value.filter(producto=>producto.id!=id)
    }
    const vaciarCarrito= (longitud)=>{
        
        carrito.value=carrito.value.splice(longitud);
    }
</script>

<template>
    <Header 
    :carrito="carrito"
    :primario="primario"
    @guardar-carrito="guardarCarrito"
    @decrementarCantidad="decrementarCantidad"
    @aumentarCantidad="aumentarCantidad"
    @eliminarProducto="eliminarProducto"
    @vaciarCarrito="vaciarCarrito">
    
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
