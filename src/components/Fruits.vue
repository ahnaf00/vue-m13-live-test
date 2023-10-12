/*
========= Computed =========
Computed property cache the data once and reuse it over and over again even though the data is used multiple time in the project. It also recalculate data when there dependent data changes  

*/

<script setup>
import { ref, computed } from 'vue';

const fruitsWithPrice = ref([
    { name: 'Apple', price: 1.20 },
    { name: 'Orange', price: 1.40 },
    { name: 'Banana', price: 1.60 },
    { name: 'Mango', price: 1.80 },
    { name: 'Pineapple', price: 2.10 },
]);

const index = ref(0); 
const fruitName = ref('');
const fruitPrice = ref(0);
// const currentFruit = ref(fruitsWithPrice[index.value]);

// const totalPrice = computed( () => {
//     let total = 0;
//     for(const fruit of fruitsWithPrice)
//     {
//         total += fruit.price
//     }

//     return total;
// })

const currentFruit = computed( () => fruitsWithPrice.value[index.value].name )

const next = () => {
    index.value = (index.value+1) % fruitsWithPrice.value.length;
    // currentFruit.value = fruitsWithPrice[index.value];
}

const add = () => {
    fruitsWithPrice.value.push({
        name:fruitName.value,
        price:fruitPrice.value
    });
    fruitName.value ='';
    fruitPrice.value= 0;
}

const totalPrice = computed(()=>{
    let total = 0;
    for(let i=0; i<fruitsWithPrice.value.length;i++)
    {
        total+=fruitsWithPrice.value[i].price;
    }
    return total;
})
</script>

<template>
    <h1 class="mb-10">Computed</h1>
    <p class="mb-5">{{ fruitsWithPrice }}</p>
    <p class="mb-2">
        Total price: {{totalPrice}}
    </p>
    <p class="mb-2">
        Index: {{ index }}
    </p>
    <p class="mb-2">
        Fruit: {{ currentFruit }}
    </p>
    <p class="mb-2">
        <!-- Price: {{ currentFruit.price }} -->
    </p>
    <p class="mt-5">
        <button @click="next()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Next Fruit
        </button>
    </p>

    
    <p>Fruit Name: <input class="my-5 p-5" v-model='fruitName'/></p>
    <p>Fruit Price: <input type="number" class="my-5 p-5" v-model='fruitPrice'/></p>
    <p class="mt-5">
        <button @click="add()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
            Add Fruit
        </button>
    </p>
</template>

<style scoped>

</style>