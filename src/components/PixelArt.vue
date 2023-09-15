<template>
<div id="pixel-art">
    <div class="section-title">
        <h4 class=" text-jade">Pixel Art</h4>
    </div>
    <div class="container">
        <div class="grid">
            
            <div v-for="(image, index) in images" class="col-3 s_col-12" :key="index">
                <div class="square"
                @click="handleClick(index)"
                >
                    <img class="square-img" :src="image.url" :alt="image.alt">
                </div>
            </div>
        </div>
    </div>
    <div v-if="showSlides" class="image-slides">
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
                <!-- @click="$refs.projectVueperSlides.goToSlide(index)" -->
                <vueper-slide v-for="(slide, index) in images" :key="index"
                @click="closeSlides"
                class="slide"
                :content="createSlide(slide)"
                />
            </vueper-slides>
        </div>
</div>
</template>

<script>
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css'

export default {
    name: 'PixelArt',
    components: { VueperSlides, VueperSlide },
    data() {
        return {
            title: 'My App is cooler than yours',
            showSlides: false,
            images: [
                {
                    url: "/images/web-portfolio/trees2.jpg",
                    alt: "Alt Text"
                },
                {
                    url: "/images/web-portfolio/dauber-logo-circle.png",
                    alt: "Alt Text"
                },
                {
                    url: "/images/web-portfolio/trees2.jpg",
                    alt: "Alt Text"
                },
                {
                    url: "/images/web-portfolio/trees2.jpg",
                    alt: "Alt Text"
                },
            ]
        }
    },
    methods: {
        log(msg) {
            console.log('Log:',msg);
        },
        handleClick(index) {
            this.showSlides = true;
            this.$refs.pixelVueperSlides.goToSlide(index);
        },
        closeSlides() {
            this.showSlides = false
        },
        createSlide(image) {
            return `<img class="slide-pic" src="${image.url}" alt="${image.alt}">`
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    .square {
        position: relative;
        width: 100%;
        overflow: hidden;
        display: block;
        padding-top: 100%;
    }
    .square::after {
        content: "";
        padding-top: 50%;
    }
    .square-img {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
    }
    .image-slides {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 4;
        cursor: zoom-out;
        backdrop-filter: blur(.5rem);
        background-color: rgba(33, 33, 33, 0.75);
        padding: 16px;
    }
    .slide {
        height: 100%;
        width: 100%
    }
    .slide-pic {
        width: 100%;
        height: 100%;
        object-fit: contain;
    }
    .image-slides .vueperslides {
        height: 100%;
    }
    .image-slides .vueperslides__inner {
        height: 100%;
    }
    .image-slides .vueperslides__parallax-wrapper {
        height: 100%;
    }
    .image-slides .vueperslide__content{
        height: 100%;
    }
</style>
