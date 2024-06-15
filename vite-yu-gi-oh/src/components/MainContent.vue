<template>
    <main>
        <div class="main-content">
            <div class="filter">
                <label for="archetype-select">Select Archetype:</label>
                <select id="archetype-select" v-model="selectedArchetype" @change="fetchCardsByArchetype">
                    <option value="">All</option>
                    <option v-for="archetype in archetypes" :key="archetype" :value="archetype">{{ archetype }}</option>
                </select>
            </div>
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
const archetypes = ref([])
const selectedArchetype = ref('')

onMounted(async () => {
    try {
        const response = await axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
        cards.value = response.data.data
        const archetypeResponse = await axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php')
        archetypes.value = archetypeResponse.data.nap(archetype => archetype.archetype_name)
    } catch (error) {
        console.error('error', error)
    }
})

const fetchCardsByArchetype = async () => {
    try {
        let url = 'https://db.ygoprodeck.com/api/v7/cardinfo.php'
        if (selectedArchetype.value) {
            url += `?archetype=${selectedArchetype.value}`
        }
        const response = await axios.get(url)
        cards.value = response.data.data
    } catch (error) {
        console.error('error', error)
    }
}
</script>

<style scoped>
    
    main{
        background-color: white;
        border: solid 80px rgb(212, 143, 56);
    }

    .main-content {
    border: solid 50px white;
    }

    .filter{
        margin-bottom: 2rem;
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