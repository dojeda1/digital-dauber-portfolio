<template>
<div id="footer">
    <h5 class="text-blue">Dream, Draw, Dev</h5>
    <div>
        <a href="https://digitaldauber.itch.io/" target="blank">
            <img class="footer-icon" src="/images/web-portfolio/icon-itch.png" alt="Itch.io Logo" />
        </a>
        <a href="https://www.instagram.com/digitaldauber/" target="blank">
            <img class="footer-icon" src="/images/web-portfolio/icon-instagram.png" alt="Instagram Logo" />
        </a>
        <a href="https://www.deviantart.com/thedigitaldauber" target="blank">
            <img class="footer-icon" src="/images/web-portfolio/icon-deviant-art.png" alt="DeviantArt Logo" />
        </a>
    </div>
    <p class="text-blue">Copyright ©{{ year }} - Dominic Ojeda</p>
</div>
</template>

<script>
export default {
    name: 'About',
    data() {
        return {
            title: 'My App is cooler than yours',
            year: "2000",
            isRotated: [
                false,
                false,
                false,
                false,
                false,
                false,
                false,
                false,
                false,
                false,
                false,
                false,
                false,
                false,
                false,
                false
            ],
        }
    },
    mounted() {
        const date = new Date()
        this.year = date.getFullYear()
    },
    methods: {
        log(msg) {
            console.log('Log:',msg);
        },
        rotate(ind) {
            const $this = this;
            if (!this.isRotated[ind]) {
                this.isRotated[ind] = true;
                setTimeout(function() {
                    $this.isRotated[ind] = false;
                },1000);
            }
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    #footer {
        padding: 15px;
        background-color: #212121;
        text-align: center;
    }
    .footer-icon {
        width: 30px;
        margin: 0 25px;
        /* transition: all .2s ease-in-out; */
    }
</style>
