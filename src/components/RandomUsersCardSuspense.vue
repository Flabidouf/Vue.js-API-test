<script setup>

import RandomUserCard from './RandomUserCard.vue';

</script>

<template>

        <Suspense>
            <template #default>
                <RandomUserCard />
            </template>
            <template #fallback>
                <div>
                    <p>Loading...</p>
                </div>
                <!-- <div class="cards spinner">
                    <NSpin size="large"/>
                </div>-->
            </template>
        </Suspense>

</template>

<style scoped>

.cards{
    height:700px;
    background-color: rgb(27, 26, 26);
    display:flex;
    justify-content:center;
    align-items:center;

}

</style>