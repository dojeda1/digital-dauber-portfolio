<template>
<div id="pixel-art">
    <div class="section-title">
        <h4 class="text-green">Pixel Art</h4>
    </div>
    <div class="container">
        <div class="grid">
            
            <div v-for="(image, index) in images" class="col-3 s_col-6" :key="index">
                <div class="square"
                @click="openSlides(index)"
                >
                    <img class="square-img" :src="image.url" :alt="image.alt">
                </div>
            </div>
        </div>
    </div>
    <SwiperModal
        ref="pixelSwiper"
        :images="images"
        :showSlides="showSlides"
        @closeModal="closeSlides"
    />
</div>
</template>

<script>
import SwiperModal from './SwiperModal.vue'

export default {
    name: 'PixelArt',
    components: { SwiperModal },
    data() {
        return {
            title: 'My App is cooler than yours',
            showSlides: false,
            images: [
                {
                    url: "/images/pixel-art/dew-drop-ruins.gif",
                    alt: "Dew Drop Ruins"
                },
                {
                    url: "/images/pixel-art/room-example.gif",
                    alt: "Symphonic Souls Room"
                },
                {
                    url: "/images/pixel-art/dungeon.gif",
                    alt: "Octobit Dungeon"
                },
                {
                    url: "/images/pixel-art/septembit.png",
                    alt: "Septembit 2023"
                },
                {
                    url: "/images/pixel-art/baddies-export.png",
                    alt: "Pocket Fables Baddies"
                },
                {
                    url: "/images/pixel-art/death.png",
                    alt: "Death"
                },
                {
                    url: "/images/pixel-art/goat-wiz-profile.png",
                    alt: "Goat Wizard"
                },
                {
                    url: "/images/pixel-art/space-cat-example.gif",
                    alt: "Space Cat"
                },
            ]
        }
    },
    methods: {
        log(msg) {
            console.log('Log:',msg);
        },
        openSlides(index) {
            this.showSlides = true;
            this.$refs.pixelSwiper.openModal(index);
        },
        closeSlides() {
            this.showSlides = false
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
