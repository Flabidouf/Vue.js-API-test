<script setup>

import RandomUserCards from './components/RandomUsersCardSuspense.vue';
import RickMortyCards from './components/RickMortyCards.vue';
import Hero from './components/Hero.vue';

import { ref } from 'vue';

const isRandomUser = ref(true);

</script>

<template>
    <main>
        <Hero 
            :isRandomUser="isRandomUser"
            @selectAPI="isRandomUser = !isRandomUser"
        />
        <KeepAlive>
            <Component :is="isRandomUser ? RandomUserCards : RickMortyCards" />
        </KeepAlive>
    </main>
</template>

