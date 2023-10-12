/*
========= Watch =========
Watch property is used to watch the changes in data properties or code and execute the custom logic that a we want to occur at a particulr stage  

*/
<script setup>
import { ref,reactive, watch } from 'vue';
const postId = ref(1);
const post = reactive({
    title: ''
})

watch(postId, (newval, oldval)=>{
    post.title = "Loading...";
    fetch(`https://jsonplaceholder.typicode.com/posts/${newval}`)
        .then(res=>res.json())
        .then(json => {
            post.title = json.title
        })
}, {immediate:true})

const fruitsWithPrice = ref([
    { name: 'Apple', price: 1.20 },
    { name: 'Orange', price: 1.40 },
    { name: 'Banana', price: 1.60 },
    { name: 'Mango', price: 1.80 },
    { name: 'Pineapple', price: 2.10 },
]);



const totalPrice = ref(0);

watch(fruitsWithPrice, (newval, oldval)=>{
    let total = 0;
    for (let i = 0; i < newval.length; i++) {
        total+=newval[i].price;
    }
    totalPrice.value = total;
}, {deep:true, immediate:true})
</script>

<template>
    <h1 class="mb-10 mt-20">Watch</h1>
    <p>{{ fruitsWithPrice }}</p>
    <p class="my-5">Price : {{ totalPrice }} </p>
    <p>
        <button @click="fruitsWithPrice.pop()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Button
        </button>
    </p>
    <p class="my-5"> 
        Post title: {{ post.title }}
    </p>
    <p class="my-5"> 
        Post ID: {{ postId }}
    </p>
    <p>
        <input type="text" class="my-5 p-5" v-model="postId">
    </p>
</template>

<style scoped>

</style>