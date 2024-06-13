<template>
    <main>
        <div class="main-content">
            <div class="card-grid">
                <Card v-for="card in cards" :key="card.id" :card="card" />
            </div>
        </div> 
    </main>
    
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import Card from './Card.vue'

const cards = ref([])

onMounted(async () => {
    try {
        const response = await axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
        cards.value = response.data.data
    } catch (error) {
        console.error('error', error)
    }
})
</script>

<style scoped>
    main{
        background-color: white;
        border: solid 80px rgb(212, 143, 56);
    }

.main-content {
    border: solid 50px white;
}

.card{
    background-color: rgb(212, 143, 56)
}

.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
    gap: 1rem;
    color: white;
    
}
</style>