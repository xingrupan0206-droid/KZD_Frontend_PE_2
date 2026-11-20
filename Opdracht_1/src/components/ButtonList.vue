<script setup>
import { onMounted, ref } from 'vue'

const categories = ref([])
const errorMessage = ref('')

onMounted(async () => {
    try {
        const response = await fetch('/assets/cat.json')

        if (!response.ok) {
            throw new Error(`Fetch failed with status ${response.status}`)
        }

        categories.value = await response.json()
    } catch (error) {
        console.error('Categorieën konden niet worden geladen:', error)
        errorMessage.value = 'Categorieën konden niet worden geladen.'
    }
})
</script>

<template>
    <section class="container py-5">
        <p v-if="errorMessage" class="alert alert-danger" role="alert">
            {{ errorMessage }}
        </p>
        <div class="row justify-content-center g-4">
            <div
                v-for="category in categories"
                :key="category.id"
                class="col-12 col-md-5"
            >
                <button type="button" class="btn btn-light border rounded-3 w-100 h-100 text-start p-3">
                    <span class="d-block fs-5 mb-2">{{ category.title }}</span>
                    <span class="d-block">{{ category.description }}</span>
                </button>
            </div>
        </div>
    </section>
</template>