<template>
<div id="illustration">
    <div class="section-title">
        <h4 class="text-green">Illustration</h4>
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
    <!-- <div v-if="showSlides" class="image-slides">
        <vueper-slides class="no-shadow"
        ref="pixelVueperSlides"
        @slide="logEvents('slide', $event)"
        :touchable="false"
        :infinite="true"
        :visible-slides="1"
        :gap="3"
        :slide-ratio="1 / 2"
        :dragging-distance="20"
        >
            <vueper-slide v-for="(slide, index) in images" :key="index"
            @click="closeSlides"
            class="slide"
            :content="createSlide(slide)"
            />
        </vueper-slides>
    </div> -->
    <SwiperModal
        ref="illustrationSwiper"
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
                    url: "/images/illustration/forest-spirit.jpeg",
                    alt: "Forest Spirit"
                },
                {
                    url: "/images/illustration/aku.jpeg",
                    alt: "Aku"
                },
                {
                    url: "/images/illustration/samus-aran.jpeg",
                    alt: "Samus Aran"
                },
                {
                    url: "/images/illustration/witch-lords.jpeg",
                    alt: "Witch Lords"
                },
                {
                    url: "/images/illustration/goodgis-vs-badgis.jpg",
                    alt: "Goodgis vs. Badgis"
                },
                {
                    url: "/images/illustration/monarch-1.jpg",
                    alt: "Monarch"
                },
                {
                    url: "/images/illustration/26-connect.jpg",
                    alt: "Angel and Demon"
                },
                {
                    url: "/images/illustration/annabelinda-full.jpg",
                    alt: "Annabelinda"
                },
                {
                    url: "/images/illustration/dragoro-full.jpg",
                    alt: "Dragoro"
                },
                {
                    url: "/images/illustration/runa-and-aitor.jpg",
                    alt: "Runa and Aitor"
                },
                {
                    url: "/images/illustration/yavelda.jpg",
                    alt: "Yavelda"
                },
                {
                    url: "/images/illustration/af.jpg",
                    alt: "Autumn Frost"
                }
            ]
        }
    },
    methods: {
        log(msg) {
            console.log('Log:',msg);
        },
        openSlides(index) {
            this.showSlides = true;
            this.$refs.illustrationSwiper.openModal(index);
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
