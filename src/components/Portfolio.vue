<template>
<div id="portfolio">
    <div class="section-title">
        <h4 class="text-green">Game Dev</h4>
    </div>
    <div class="container">
        <div class="section-header">
            <h5 class=" text-green">Select a Game</h5>
        </div>
            <!-- @ready="logEvents('ready', $event)"
            @previous="logEvents('previous', $event)"
            @next="logEvents('next', $event)"
            @before-slide="logEvents('before-slide', $event)" -->
        <div class="paint-pics">
            <vueper-slides class="no-shadow"
            ref="projectVueperSlides"
            @slide="logEvents('slide', $event)"
            :touchable="false"
            :infinite="true"
            :visible-slides="5"
            :gap="3"
            :slide-ratio="1 / 5"
            :dragging-distance="20"
            :breakpoints="{
                1000: {
                    visibleSlides: 3,
                    slideRatio: 1 / 3
                },
                600: {
                    visibleSlides: 2,
                    slideRatio: 1 / 2,
                    touchable: true,
                    arrows: false,
                } 
            }">
                <vueper-slide v-for="(slide, index) in projects" :key="index"
                class="paint-pic-container"
                :class="{ 'active': slide.isActive}"
                @click="$refs.projectVueperSlides.goToSlide(index)"
                :content="createSlide(slide)"
                >
                
                </vueper-slide>
            </vueper-slides>
        </div>
        <div class="section-header">
            <h5 class=" text-green">Game Summary</h5>
        </div>
        <div class="grid">
            <div class="col-8 s_col-12">
                <h5>{{ currentProject.title }}</h5>
                <img class="portfolio-devices" :src="currentProject.mockup" alt="Mockup">
                <div class="dual-buttons">
                <a target="_blank" :href="currentProject.visit">
                    <button class="btn">{{ currentProject.btnText }}<i className="material-icons right">public</i></button>
                </a>
                <a v-if="currentProject.code" target="_blank" :href="currentProject.code">
                    <button class="btn">Code<i className="material-icons right">code</i></button>
                </a>
                </div>
            </div>
            <div class="col-4 s_col-12">
                <h6 class=" text-green">- About the Game -</h6>
                <p>{{ currentProject.sum }}</p>
                <h6 class=" text-green">- Tags -</h6>
                <p>
                    <span v-for="item in currentProject.list"
                    :key="item" 
                    class="tag">
                        {{ item }}
                    </span>
                </p>
            </div>
            <div class="col-4 s_col-12">
                <img class="preview-img" alt="Screenshot 1"
                :src="currentProject.img1"
                @click="openSlides(0)">
            </div>
            <div class="col-8 row-2 s_col-12">
                <img class="preview-img" alt="Screenshot 2"
                :src="currentProject.img2"
                @click="openSlides(1)">
            </div>
            <div class="col-4 s_col-12">
                <img class="preview-img" alt="Screenshot 3"
                :src="currentProject.img3"
                @click="openSlides(2)">
            </div>
        </div>
    </div>
    <!-- <div v-if="imageModal != ''" class="image-modal"
    @click="zoomImage('')">
        <img :src="imageModal" alt="zoomed image">
    </div> -->
    <SwiperModal
        ref="pixelSwiper"
        :images="images"
        :showSlides="showSlides"
        @closeModal="closeSlides"
    />
</div>
</template>

<script>
// In your Vue.js component.
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css'
import SwiperModal from './SwiperModal.vue'

export default {
    name: 'Portfolio',
    // components: { VueperSlides, VueperSlide },
    components: { VueperSlides, VueperSlide, SwiperModal },
    data() {
        return {
            currentProject: {},
            imageModal: '',
            showSlides: false,
            // slides: [
            //     {
            //     title: 'Slide #1',
            //     content: 'Slide content.'
            //     },
            //     {
            //     title: 'Slide #2',
            //     content: 'Slide content.'
            //     },
            //     {
            //     title: 'Slide #3',
            //     content: 'Slide content.'
            //     },
            // ],
            projects: [
                {
                    title: "Dino Mayhem",
                    mockup: "/images/dino-mayhem/screen-1.png",
                    paint: "/images/dino-mayhem/cover.png",
                    img1: "/images/dino-mayhem/screen-4.png",
                    img2: "/images/dino-mayhem/screen-2.png",
                    img3: "/images/dino-mayhem/screen-3.png",
                    visit: "https://store.steampowered.com/app/2614930/Dino_Mayhem/",
                    btnText: "Wishlist",
                    code: "",
                    sum: "Cause mayhem in this retro platformer by devouring people and destroying vehicles to earn points. Eating people not only satisfies your appetite for destruction but also helps you regain health, and chowing down on goats provides an even bigger health boost. Test your survival skills as you navigate the urban jungle, aiming to last as long as possible and rack up those high scores. Endure the chaos as long as you can to unlock new skins. Slated for a full Steam release in 2026.",
                    list: ["Godot", "Aseprite", "Arcade", "Platformer", "Unlockables", "Steam", "commercial"],
                    isActive: true
                },
                {
                    title: "Matchy Dice",
                    mockup: "/images/matchy-dice/screen-1.png",
                    paint: "/images/matchy-dice/banner.png",
                    img1: "/images/matchy-dice/screen-2.png",
                    img2: "/images/matchy-dice/screen-3.png",
                    img3: "/images/matchy-dice/screen-4.png",
                    visit: "https://digitaldauber.itch.io/matchy-dice",
                    btnText: "View",
                    code: "",
                    sum: "A thrilling, match-3 style puzzle challenge. Your objective is to match three dice of the same value by swapping dice left or right, but not up or down! Keep an eye out for those pesky black dice; they can't be swapped directly, but you can change them by hitting the 'Roll Dice' button. Race against time as the dice stack up, aiming to score as many points as possible before they reach the top. Can you master the art of dice swapping and achieve the highest score in ‘Match’ Dice? Made for the GMTK Jam.",
                    list: ["Godot", "Aseprite", "Arcade", "Match 3", "Mobile Friendly", "Web"],
                    isActive: false
                },
                {
                    title: "Pupkin Patch",
                    mockup: "/images/pupkin-patch/screen-1.png",
                    paint: "/images/pupkin-patch/cover.png",
                    img1: "/images/pupkin-patch/screen-2.png",
                    img2: "/images/pupkin-patch/screen-3.png",
                    img3: "/images/pupkin-patch/screen-1.png",
                    visit: "https://digitaldauber.itch.io/pupkin-patch",
                    btnText: "View",
                    code: "",
                    sum: "Take care of the adorable Pupkin to learn more about its mysterious origins. Point and click to interact with the Pupkin. Move items from your inventory to the ground to have the Pupkin interact with them. Gather and sell items to earn more money. Purchase various items for your Pupkin at the Shop. Made for the Cozy Autumn Game Jame",
                    list: ["Godot", "Aseprite", "Tamagotchi", "Web"],
                    isActive: false
                },
                {
                    title: "Shark Dentist",
                    mockup: "/images/shark-dentist/screen-1.png",
                    paint: "/images/shark-dentist/title-image.png",
                    img1: "/images/shark-dentist/screen-1.png",
                    img2: "/images/shark-dentist/screen-2.png",
                    img3: "/images/shark-dentist/screen-3.png",
                    visit: "https://digitaldauber.itch.io/shark-dentist",
                    btnText: "View",
                    code: "",
                    sum: "Who does a shark go to when they need dental car? That would be you, the Shark Dentist. In this fast-paced game, you're armed with only your handy toothbrush and forceps. Brush and extract those troublesome dental issues as they pop up, keeping the shark's bills climbing higher and higher. With reflexes and precision, you'll aim to be the top shark dentist in town, at least until an angry patient chomps you down. Made for the Global Game Jam.",
                    list: ["Godot", "Aseprite", "Arcade", "Web"],
                    isActive: false
                },
                {
                    title: "Sneaky Sheep",
                    mockup: "/images/sneaky-sheep/screen-1.png",
                    paint: "/images/sneaky-sheep/cover.png",
                    img1: "/images/sneaky-sheep/screen-2.png",
                    img2: "/images/sneaky-sheep/screen-3.png",
                    img3: "/images/sneaky-sheep/screen-4.png",
                    visit: "https://digitaldauber.itch.io/sneakysheep",
                    btnText: "View",
                    code: "",
                    sum: "As a literal wolf in sheep's clothing, your mission is to sneak around the farm and devour all the sheep before the sheep discover the truth. With stealth and strategy, you'll navigate the pen, using deceptive 'baaahs' and obstacles to stay out of sight. Can you outsmart the sheep and satisfy your hunger for mutton? Find out in 'Sneaky Sheep'! Made for the SLC Game Devs Jam.",
                    list: ["Godot", "Aseprite", "Stealth", "Windows", "Mac"],
                    isActive: false
                },
                {
                    title: "Pack Hunters",
                    mockup: "/images/pack-hunters/screen-1.png",
                    paint: "/images/pack-hunters/cover.png",
                    img1: "/images/pack-hunters/screen-2.png",
                    img2: "/images/pack-hunters/screen-3.png",
                    img3: "/images/pack-hunters/screen-4.png",
                    visit: "https://synsugarstudio.itch.io/uigj-2022",
                    btnText: "View",
                    code: "",
                    sum: "Embark on a dungeon-crawling journey filled with adorable animal warriors and Zelda-style gameplay. Clear each room of menacing enemies and add new furry allies to your pack as you progress. Can you defeat all 10 rooms? To be honest, I can’t... Made for the Utah Indie Game Jam. Worked as part of a team, creating all the visual assets and assisting with the code.",
                    list: ["Godot", "Aseprite", "Dungeon Crawler", "Team Project", "Action", "Web"],
                    isActive: false
                }
            ]
        }
    },
    methods: {
        log(msg) {
            console.log('Log:',msg);
        },
        logEvents (eventName, params) {
            console.log(eventName, params)
            console.log('Index:',params.currentSlide.index)
            this.swapProject(params.currentSlide.index)
        },
        swapProject(ind) {
            console.log(ind)
            console.log(this.projects[ind])
            this.currentProject = this.projects[ind];
            this.projects.forEach(project => project.isActive = false)
            this.projects[ind].isActive = true;
        },
        // zoomImage(src) {
        //     console.log('hey');
        //     this.imageModal = src;
        // },
        createSlide(project) {
            return `
            <img class="paint-pic" src="${project.paint}" alt="Painted Preview">
            <p>${project.title}</p>
        `
        },
        openSlides(index) {
            this.showSlides = true;
            this.$refs.pixelSwiper.openModal(index);
        },
        closeSlides() {
            this.showSlides = false
        }
    },
    computed: {
        images() {
            return [
                {
                    url: this.currentProject.img1,
                    alt: "game screenshot"
                },
                {
                    url: this.currentProject.img2,
                    alt: "game screenshot"
                },
                {
                    url: this.currentProject.img3,
                    alt: "game screenshot"
                }
            ]
        }
    },
    created: function() {
        this.swapProject(0);
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    .preview-img {
        height: 100%;
        width: 100%;
        transition: all .2s ease-in-out;
        box-shadow: 0 4px 5px 0 rgb(0 0 0 / 14%), 0 1px 10px 0 rgb(0 0 0 / 12%), 0 2px 4px -1px rgb(0 0 0 / 30%);
        cursor: zoom-in;
        object-fit: cover;
    }
    .preview-img:hover {
        opacity: .8;
    }
    .image-modal {
        cursor: zoom-out;
        backdrop-filter: blur(.5rem);
        position: fixed;
        z-index: 4;
        top: 0;
        left: 0;
        background-color: rgba(33, 33, 33, 0.75);
        height: 100%;
        width: 100%;
        padding: 16px;
    }
    .image-modal img {
        object-fit: contain;
        height: 100%;
        width: 100%;
    }
    .portfolio-devices {
        width: 100%;
        margin-bottom: 1rem;
    }
    .paint-pics {
        padding: 0 40px;
        width: 100%;
        overflow: hidden;
    }
    .paint-pic-container {
        cursor: pointer;
        padding: 10px;
    }
    .paint-pic {
        width: 100%;
        transition: all .2s ease-in-out;
    }
    .paint-pic-container:hover .paint-pic{
        transform: translateY(-5px);
        transform: scale(1.1);
    }
    .paint-pic-container.active {
        color: #8dc63f;
    }
    .tag {
        display: inline-block;
        text-transform: lowercase;
        /* color: white; */
        /* background-color: #8dc63f;
        background-color: #212121; */
        background-color: lightgray;
        padding: 2px 6px;
        margin: 2px 2px;
        font-size: 14px;
        border-radius: 4px;
    }
</style>
