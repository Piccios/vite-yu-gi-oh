<template>
    <div class="card">
        <img :src="card.card_images[0].image_url" :alt="card.name" />
        <h2>{{ card.name }}</h2>
        <p>{{ card.desc }}</p>
    </div>
</template>

<script setup>
defineProps({
    card: Object
})
</script>

<style scoped>
.card {
    border: 1px solid #ccc;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s;
}

.card:hover {
    transform: translateY(-5px);
}

.card img {
    width: 100%;
    height: auto;
}

.card h2 {
    font-size: 1.2rem;
    margin: 0.5rem 0;
}

.card p {
    font-size: 0.9rem;
    color: #666;
    padding: 0 1rem 1rem;
}
</style>