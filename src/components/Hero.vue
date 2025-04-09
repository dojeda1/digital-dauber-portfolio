<template>
    <div id="hero">
        <img class="hero-image" src="/images/web-portfolio/dino-portrait-overlay.png" alt="dino portrait">
        <div class="gradient"></div>
        <div class="hero-elements">
            <img class="hero-logo" src="/images/web-portfolio/dauber-logo-circle.png" alt="D Logo" />
            <h1 class="white-text font2">Digital Dauber</h1>
            <h5 class="font1 text-green">Digital Artist & Game Dev</h5>
            <div class="hero-icons">
            <a href="https://digitaldauber.itch.io/" target="blank">
                <img class="hero-icon" src="/images/web-portfolio/icon-itch.png" alt="Itch.io Logo" />
            </a>
            <a href="https://www.instagram.com/digitaldauber/" target="blank">
                <img class="hero-icon" src="/images/web-portfolio/icon-instagram.png" alt="Instagram Logo" />
            </a>
            <a href="https://www.deviantart.com/thedigitaldauber" target="blank">
                <img class="hero-icon" src="/images/web-portfolio/icon-deviant-art.png" alt="DeviantArt Logo" />
            </a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Hero'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    #hero {
        /* -webkit-filter: grayscale(100%);
        filter: grayscale(100%); */
        height: 100%;
        min-height: 500px;
        padding: 20px;
        /* background-color: #2bb673; */
        /* background:linear-gradient(0deg, rgba(64, 64, 64, 0.8), rgba(125, 125, 125, 0.8)), url('/images/web-portfolio/dino-portrait-full.png'); */

        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        color: white;
        text-align: center;
        /* background-position: center;
        background-size: cover; */
        overflow: hidden;
        position: relative;
    }

    #heroo::before {
        content: "";
        position: absolute;
        top: 50%;  /* position the top  edge of the element at the middle of the parent */
        left: 50%; /* position the left edge of the element at the middle of the parent */
        transform: translate(-50%, -50%);
        width: 100%;
        height: 100%;
        background:linear-gradient(0deg, rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.8)), url('/images/web-portfolio/dino-portrait-full.png');
        filter: grayscale(100%);
    }

    .hero-image {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
        /* background:linear-gradient(0deg, rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.8)), url('/images/web-portfolio/dino-portrait-full.png'); */
        filter: grayscale(100%);
    }

    .gradient {
        position: absolute;
        top: 0;  /* position the top  edge of the element at the middle of the parent */
        left: 0; /* position the left edge of the element at the middle of the parent */
        width: 100%;
        height: 100%;
        background:linear-gradient(0deg, rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.6));
    }

    .hero-elements {
        position: relative;
    }

    .hero-logo {
        width: 200px;
        margin: 0 25px 1rem 0;
    }

    .hero-icons {
        margin-top: 1rem;
    }

    .hero-icon {
        width: 60px;
        margin: 0 25px;
        transition: all .2s ease-in-out;
    }
    .hero-icon:hover {
        transform: translateY(-5px) scale(1.2);
    }

    @media only screen and (max-width: 600px) {
        #hero {
            min-height: unset;
        }
        .hero-logo {
            display: none;
        }
    }
</style>
