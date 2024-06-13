<template>
    <div class="main-content">
        <div class="card-grid">
            <Card v-for="card in cards" :key="card.id" :card="card" />
        </div>
    </div>
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
        console.error('error:', error)
    }
})
</script>

<style scoped>
.main-content {
    padding: 2rem;
}

.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1rem;
}
</style>