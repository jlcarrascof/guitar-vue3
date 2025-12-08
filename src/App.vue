<script setup>
    import { ref, reactive, onMounted } from 'vue';
    import { db } from './data/guitars';
    import Guitar from './components/Guitar.vue';

    const guitars = ref([]);
    const cart = ref([]);

    onMounted(() => {
        guitars.value = db
    })

   const addCart = (guitar) => {
        guitar.cantidad = 1;
        cart.value.push(guitar);
   };
</script>

<template>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <Guitar 
                v-for="guitar in guitars"
                :guitar="guitar"
                @add-cart="addCart"
            />
        </div>
    </main>


    <footer class="bg-dark mt-5 py-5">
        <div class="container-xl">
            <p class="text-white text-center fs-4 mt-4 m-md-0">GuitarLA - Todos los derechos Reservados</p>
        </div>
    </footer>
</template>
