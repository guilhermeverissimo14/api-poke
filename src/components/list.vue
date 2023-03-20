<script setup>
const pokemon = defineProps(["name", "url"])
</script>

<template>
    <div class="col-4">
        <div class="card mb-2">
            <p class="text-center">{{ pokemon.name }}</p>
            <img :src="url" alt="pokemon" />
        </div>
    </div>
</template>

<style></style>

