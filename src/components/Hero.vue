
<script setup> 

import { defineProps, defineEmits } from 'vue';


const emit = defineEmits([ 
    'selectAPI'
])
const emitSelectedAPI = () => {
    emit('selectAPI')
}


const {isRandomUser} = defineProps([
    'isRandomUser'
])   



</script>


<template>

    <div class="hero">
        <h1>{{isRandomUser ? 'Random Users' : 'Rick and Morty'}}</h1>
        <p @click="emitSelectedAPI">{{isRandomUser ? 'Rick and Morty' : 'Random Users'}}</p>
    </div>

</template>

<style scoped>
.hero {
    height : 40vh;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    flex-direction: column
}
.hero img {
    position: absolute;
    height: 700px;
    opacity: 0.1;
}
.hero h1 {
    font-size: 100px;
    font-weight: bold;
}
.hero p {
    cursor: pointer;
}

</style>