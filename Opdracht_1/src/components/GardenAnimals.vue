<script setup>
import { onMounted, ref } from 'vue'

const animals = ref([])
const isLoading = ref(true)
const errorMessage = ref('')

const animalNames = [
    'hedgehog',
    'rabbit',
    'squirrel',
    'frog',
    'robin',
    'blackbird',
    'butterfly',
    'bee',
]

onMounted(async () => {
    const apiKey = import.meta.env.VITE_API_NINJAS_KEY

    if (!apiKey) {
        errorMessage.value = 'API-key ontbreekt. Voeg VITE_API_NINJAS_KEY toe aan .env.local.'
        isLoading.value = false
        return
    }

    try {
        const results = await Promise.all(
            animalNames.map(async (name) => {
                const url = new URL('https://api.api-ninjas.com/v1/animals')
                url.searchParams.set('name', name)

                const response = await fetch(url, {
                    headers: { 'X-Api-Key': apiKey },
                })

                if (!response.ok) {
                    throw new Error(`Animals API request failed (${response.status})`)
                }

                const data = await response.json()
                return Array.isArray(data) ? data[0] : null
            }),
        )

        animals.value = results.filter((animal) => animal && animal.name)

        if (animals.value.length === 0) {
            throw new Error('The Animals API returned no animals.')
        }
    } catch (error) {
        console.error('Dieren konden niet worden geladen:', error)
        errorMessage.value = 'Dieren konden niet worden geladen. Controleer je API-key en probeer opnieuw.'
    } finally {
        isLoading.value = false
    }
})
</script>

<template>
    <section class="container py-5">
        <h2 class="text-light mb-4">Dieren in de tuin</h2>

        <p v-if="isLoading" class="text-light" role="status">Dieren laden...</p>
        <p v-else-if="errorMessage" class="alert alert-danger" role="alert">
            {{ errorMessage }}
        </p>

        <div v-else class="row g-4">
            <div v-for="animal in animals" :key="animal.name" class="col-12 col-md-6 col-lg-4">
                <article class="card h-100">
                    <div class="card-body">
                        <h3 class="card-title h5">{{ animal.name }}</h3>
                        <p class="card-text mb-1">
                            <strong>Habitat:</strong>
                            {{ animal.characteristics?.habitat || 'Onbekend' }}
                        </p>
                        <p class="card-text mb-1">
                            <strong>Voedsel:</strong>
                            {{ animal.characteristics?.diet || 'Onbekend' }}
                        </p>
                        <p class="card-text mb-0">
                            <strong>Locatie:</strong>
                            {{ animal.locations?.join(', ') || 'Onbekend' }}
                        </p>
                    </div>
                </article>
            </div>
        </div>
    </section>
</template>
