<script setup>
    import { ref, reactive, onMounted } from 'vue';
    import { db } from './data/guitars';
    import Guitar from './components/Guitar.vue';
    import Header from './components/Header.vue';
    import Footer from './components/Footer.vue';

    const guitars = ref([]);
    const cart = ref([]);
    const guitar = ref({});

    onMounted(() => {
        guitars.value = db
        guitar.value = db[3];
    })

   const addCart = (guitar) => {
        const existCart = cart.value.findIndex(product => product.id === guitar.id);

        if (existCart >= 0) {
            cart.value[existCart].cantidad++;
        } else {
            guitar.cantidad = 1;
            cart.value.push(guitar);
        }

   };

   const decrementQuantity = (id) => {
        const index = cart.value.findIndex(product => product.id === id);
        if (cart.value[index].cantidad <= 1) return;
        cart.value[index].cantidad--; 
   }

   const incrementQuantity = (id) => {
        const index = cart.value.findIndex(product => product.id === id);
        if (cart.value[index].cantidad >= 5) return;
        cart.value[index].cantidad++;    
   }

   const deleteProduct = (id) => {
        cart.value = cart.value.filter(product => product.id !== id)
   }

   const emptyCart = () => {
       cart.value = [];
   }

</script>

<template>
    <Header 
        :cart="cart"
        :guitar="guitar"
        @increment-quantity="incrementQuantity"
        @decrement-quantity="decrementQuantity"
        @add-cart="addCart"
        @delete-product="deleteProduct"
    />
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
