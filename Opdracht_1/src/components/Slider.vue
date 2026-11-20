<script setup>
import sliderImage from '@/assets/Slider_website.jpg'
</script>

<template>
    <section class="container py-5">
        <div class="row align-items-center justify-content-between g-4 slider-content">
            <div class="col-12 col-md-5">
                <h1 class="text-light">Fresh Flowers, Thoughtfully Arranged</h1>
                <p class="text-light">
                    Seasonal blooms crafted for everyday moments and meaningful occasions.
                    Sourced responsibly and arranged with care.
                </p>
                <button type="button" class="btn btn-primary">Shop Flowers</button>
            </div>

            <div class="col-12 col-md-5">
                <div id="flowerCarousel" class="carousel slide">
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img :src="sliderImage" class="d-block w-100 slider-image" alt="A young plant growing in someone's hands">
                            <div class="carousel-caption">
                                <h2 class="h4 mb-1">Indoor Plants</h2>
                                <p class="mb-0">Greenery for your home and office</p>
                            </div>
                        </div>
                        <div class="carousel-item">
                            <img :src="sliderImage" class="d-block w-100 slider-image" alt="A young plant growing in someone's hands">
                            <div class="carousel-caption">
                                <h2 class="h4 mb-1">Fresh Flowers</h2>
                                <p class="mb-0">Seasonal blooms for every occasion</p>
                            </div>
                        </div>
                        <div class="carousel-item">
                            <img :src="sliderImage" class="d-block w-100 slider-image" alt="A young plant growing in someone's hands">
                            <div class="carousel-caption">
                                <h2 class="h4 mb-1">Thoughtful Gifts</h2>
                                <p class="mb-0">A little something to brighten their day</p>
                            </div>
                        </div>
                    </div>

                    <button class="carousel-control-prev" type="button" data-bs-target="#flowerCarousel" data-bs-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="visually-hidden">Previous</span>
                    </button>
                    <button class="carousel-control-next" type="button" data-bs-target="#flowerCarousel" data-bs-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="visually-hidden">Next</span>
                    </button>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
.slider-content {
    min-height: 60vh;
}

.slider-image {
    aspect-ratio: 3 / 2;
    object-fit: cover;
}

.carousel-caption {
    text-shadow: 0 1px 4px rgb(0 0 0 / 80%);
}
</style>
