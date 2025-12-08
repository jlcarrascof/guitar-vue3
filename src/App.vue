<script setup>
    import { ref, reactive, onMounted } from 'vue';
    import { db } from './data/guitars';
    import Guitar from './components/Guitar.vue';
    import Header from './components/Header.vue';
    import Footer from './components/Footer.vue';

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
    <Header />
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

    <Footer />
</template>
