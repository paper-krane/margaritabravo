<script setup>
import gsap from 'gsap';
import { ref, onMounted } from 'vue';
import { ScrollTrigger } from 'gsap/all';

// import bannerImage from '@/assets/video-banner.webp';
import bannerVideo from '@/assets/margarita-bravo.mp4';

// Refs
const heroImageContainer = ref(null);
const heroImageWrapRef = ref(null);
const ctx = ref(null);

onMounted(() => {
    gsap.registerPlugin(ScrollTrigger);

    // Context
    ctx.value = gsap.context(() => {        
        // Parallax Background Image
        gsap.to(heroImageWrapRef.value, {
            scrollTrigger: {
                trigger: heroImageContainer.value,
                scrub: true,
            },
            y: '30%',
            ease: 'none',
        });
    });
})
</script>


<template>
    <section class="pk__video-banner_section pk__section-margnin-top pk__section-margnin-bot pk__section-padding-top pk__section-padding-bot" ref="heroImageContainer">
        <div class="pk__video-banner_video" ref="heroImageWrapRef">
            <video autoplay muted loop playsinline>
                <source :src="bannerVideo" type="video/mp4" />
            </video>
        </div>
    </section>
</template>


<style lang="scss">
@import "@/assets/_variables";

.pk__video-banner_section {
    position: relative;
    height: 65svh;
    background-color: $font-color;
    overflow: hidden;

    .pk__video-banner_video {
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 130%;
        overflow: hidden;

        video {
            width: 100%;
            height: 100%;
            object-fit: cover;
            object-position: 50% 80%;
            opacity: .75;
            filter: contrast(1.75) brightness(80%);
            -webkit-filter: brightness(100%);
        }
    }
}
</style>