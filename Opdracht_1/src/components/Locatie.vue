<script setup>
import shopImage from '@/assets/Slider_website.jpg'
</script>

<template>
    <footer class="container py-5 text-light">
        <div class="row align-items-center g-4">
            <div class="col-12 col-md-6">
                <img :src="shopImage" class="img-fluid w-100 shop-image" alt="Plant growing in a garden">
            </div>

            <div class="col-12 col-md-6">
                <h2 class="h4">Visit Our Shop</h2>
                <address class="mb-3">
                    123 Flower Street<br>
                    Garden District<br>
                    Bloomtown, BT 45678
                </address>
                <p class="mb-0">
                    Open Monday to Saturday<br>
                    9:00 AM – 6:00 PM
                </p>
            </div>
        </div>

        <div class="row mt-4">
            <div v-for="social in ['Instagram', 'Facebook', 'Pinterest', 'Twitter']"
                :key="social"
                class="col-6 col-md-3">
                <span>{{ social }}</span>
            </div>
        </div>
    </footer>
</template>

<style scoped>
.shop-image {
    max-height: 300px;
    object-fit: cover;
}
</style>