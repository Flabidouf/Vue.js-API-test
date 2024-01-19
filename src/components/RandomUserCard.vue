<script setup>
    import axios from 'axios';
    import { ref, watch } from 'vue';
    import Card from './Card.vue';

    const characters = ref([]);
    const page = ref(1) // Because the API has a 1-based index
    const isLoading = ref(false)

  
    const fetchRandomUsers = async () => {
        isLoading.value = true;
        await new Promise(resolve => setTimeout(resolve, 1000))
        try{
            const response = await axios.get(`https://randomuser.me/api/?page=${page.value}&results=8&seed=abc`)
            characters.value =  response.data.results  //[...characters.value, ...response.data.results]
            console.log(characters.value)
        } catch (error) {
            console.error("Error fetching random users", error)
        } finally {
            isLoading.value = false;
        }
        
    }

    watch(page, () => {
        fetchRandomUsers()
    })

    fetchRandomUsers()


</script>

<template>

    <div class="container">
        <div class="cards" >
            <Card
            v-for="character in characters"
                :key="character.login.uuid"
                :image="character.picture.large"
                :name="`${character.name.first} ${character.name.last}`"
            >
                <div>
                    <div class="location">
                        <p>{{`${character.location.city}, ${character.location.country}`}}</p>
                    </div>
                </div>
            </Card>
        </div>
       
            <div v-if="isLoading" class="cards spinner">
                <NSpin size="large"/>
            </div>
        
        <div class="button-container">
            <button @click="page--">&lt</button>
            <button @click="page++">></button>
        </div>
    </div>
    
</template>

<style scoped>
.container {
    background-color: rgb(27, 26, 26);
    padding: 30px
}
.cards {
    max-width: 1000px;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;
}
.cards h3 {
    font-weight: bold;
}
.cards p {
    font-size: 10px;
}

.button-container {
    display: flex;
    justify-content: center;
    padding-top: 30px
}
.button-container button {
    border: none;
    width: 50px;
    height: 50px;
    border-radius: 100%;
    margin: 0 5px;
    cursor: pointer;
}
.spinner {
    display: flex;
    align-items: center;
    justify-content: center;
}
p{
    font-size: 10px;
}

.location{
    display: flex;
    flex-wrap: wrap;
}

</style>
