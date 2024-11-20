<template>
    <div class="card__glider">
        <div :class="`glide-${index}`">
            <div class="glide__track" data-glide-el="track">
                <ul class="glide__slides">

                    <div v-for="(cardItem, index) in cardContent" :key="index">

                        <li class="glide__slide">
                            <div class="card-content">
                                <img v-if="cardItem.image"
                                class="card-content__image"
                                :src="cardItem.image"
                                :alt="`Card_Image_${index + 1}`"
                                >
                                <div v-if="cardItem.number" class="card-content--with-number">
                                    <h1 class="card-content__number">
                                        {{ cardItem.number }}
                                    </h1>
                                    <h3 class="card-content__text">
                                        {{ cardItem.text }}
                                    </h3>
                                </div>
                                <div v-else-if="cardItem.text" class="card-content--without-number">
                                    <h3 class="card-content__text" v-html="cardItem.text">
                                    </h3>
                                </div>
                            </div>
                        </li>
                        
                    </div>
                </ul>
                <div class="glide__bullets" data-glide-el="controls[nav]">
                    <button v-for="(cardItem, index) in cardContent" :key="index" class="glide__bullet" :data-glide-dir="`${index}`">
                        <span class="glide__bullet-reaction"></span>
                    </button>
                </div>
            </div>
        </div>   
    </div>
</template>

<script>
    import Glide from '@glidejs/glide';

    export default {
    name: "CardGlider",
    props: {
        cardContent: {
            type: Array,
            required: true
        },
        index: {
            type: Number,
            required: true
        }
    },
    data() { 
        return {
            currentBulletPosition: 0,
            bullets: [],
            bulletReactions: [],
            loadingCancelled: true,
            transitionDelay: 5000,
        };
    },
    mounted() {
        this.setGlider();
        this.setBullets();
    }, 
    methods: {
        setBullets() {
            this.bullets = Array.from(document.querySelectorAll(`.glide-${this.index} .glide__bullet`));
            this.bulletReactions = Array.from(document.querySelectorAll(`.glide-${this.index} .glide__bullet .glide__bullet-reaction`));
            this.bulletReactions[0].classList.remove('glide__bullet-reaction--fill');
        },
        setGlider() {
            const config = {
                type: 'carousel',
                startAt: 0,
                perView: 1,
                autoplay: 2000,
                gap: 0

            }
            let currentGlide = new Glide('.glide-'+this.index, config).mount({})
            currentGlide.pause();

            // Add event listeners to handle hover behavior
            const glideElement = document.querySelector(`.glide-${this.index}`);

            // Pause on mouse enter (hover)
            glideElement.addEventListener('mouseover', () => {
                this.startLoading(currentGlide);
            });

            // Resume on mouse leave
            glideElement.addEventListener('mouseleave', () => {
                this.stopLoading(currentGlide);
            });
        },
        startLoading(currentGlide){
            this.loadingCancelled = false;
            this.startBulletTransition();
            currentGlide.play(3000);
        },
        stopLoading(currentGlide) {
            currentGlide.pause();
            this.loadingCancelled = true;
        },
        async startBulletTransition() {
                const currentBulletReaction = this.bulletReactions[this.currentBulletPosition];
                this.bulletReactions[this.currentBulletPosition].classList.add('glide__bullet-reaction--fill');

                const currentBullet = this.bullets[this.currentBulletPosition];

                // Wait 5 seconds for the loading to complete, or until it is canceled
                const loadingComplete = await new Promise((resolve) => {
                    const timeout = setTimeout(() => {
                        resolve(true); // Loading completed successfully
                        clearInterval(checkForCancel);
                    }, 3000);

                    const checkForCancel = setInterval(() => {
                        if (this.loadingCancelled) {
                            clearTimeout(timeout); // Cancel the timeout
                            clearInterval(checkForCancel);
                            this.resetCurrentBullet(currentBulletReaction);
                            resolve(false); // Indicate that loading was cancelled
                        }
                    }, 100);
                });

                if (loadingComplete) {
                    this.setVisitedBullet(currentBullet);
                    this.resetCurrentBullet(currentBulletReaction);
                    this.currentBulletPosition = (this.currentBulletPosition+1)%(this.bullets.length);
                    if(this.currentBulletPosition == 0){
                        this.resetAllBullets();
                    }
                }
        },
        setVisitedBullet(currentBullet) {
            currentBullet.classList.add('glide__bullet--visited')
        },
        resetCurrentBullet(currentBulletReaction) {
            currentBulletReaction.classList.remove('glide__bullet-reaction--fill');
        },
        resetAllBullets() {
            this.bullets.forEach((bullet) => {
                bullet.classList.remove('glide__bullet--visited');
            });
        }
    }   
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
</style>