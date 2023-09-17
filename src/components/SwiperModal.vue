<template>
    <div v-show="showSlides" class="image-slides">
        <vueper-slides class="no-shadow"
        ref="swiperImageModal"
        :touchable="false"
        :infinite="true"
        :visible-slides="1"
        :gap="3"
        :slide-ratio="1 / 2"
        :dragging-distance="20"
        >
            <!-- @click="$refs.projectVueperSlides.goToSlide(index)" -->
            <vueper-slide v-for="(slide, index) in images" :key="index"
            @click="closeModal"
            class="slide"
            :content="createSlide(slide)"
            />
        </vueper-slides>
    </div>
</template>

<script>
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css'

export default {
    name: 'SwiperModal',
    components: { VueperSlides, VueperSlide },
    props: {
        images: {
            type: Array,
            default() {
                return []
            }
        },
        showSlides: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            title: 'My App is cooler than yours',
        }
    },
    methods: {
        log(msg) {
            console.log('Log:',msg);
        },
        openModal(index) {
            console.log('index: ', index);
            // this.showSlides = true;
            // this.$emit('openModal')
            this.$refs.swiperImageModal.goToSlide(index);
        },
        closeModal() {
            // this.showSlides = false
            this.$emit('closeModal')
        },
        createSlide(image) {
            return `<img class="slide-pic" src="${image.url}" alt="${image.alt}">`
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
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
    .image-slides .vueperslides__arrow--prev {
        left: -16px;
    }
    .image-slides .vueperslides__arrow--next {
        right: -16px;
    }
</style>
