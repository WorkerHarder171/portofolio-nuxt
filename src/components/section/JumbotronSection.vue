<script setup>
import { ref, onMounted } from "vue";
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";

const firstText = ref(null);
const secondText = ref(null);
const slider = ref(null);

let xPercent = 0;
let direction = -1;

const animate = () => {
  if (xPercent < -100) {
    xPercent = 0;
  } else if (xPercent > 0) {
    xPercent = -100;
  }
  gsap.set(firstText.value, { xPercent });
  gsap.set(secondText.value, { xPercent });
  requestAnimationFrame(animate);
  xPercent += 0.1 * direction;
};

onMounted(() => {
  gsap.registerPlugin(ScrollTrigger);
  gsap.to(slider.value, {
    scrollTrigger: {
      trigger: document.documentElement,
      scrub: 0.25,
      start: 0,
      end: window.innerHeight,
      onUpdate: (e) => {
        direction = e.direction * -1;
      },
    },
    x: "-500px",
  });
  requestAnimationFrame(animate);
});
</script>

<template>
  <div class="min-h-screen bg-black p-24">
    <div
      class="flex flex-col items-center justify-between border border-gray-700 rounded-xl h-[760px] w-full"
    >
      <!-- Header -->
      <div
        class="wrapper-header rounded-t-[10px] text-[#dedede] px-10 w-full h-[520px] flex items-center justify-center text-2xl"
      >
        <div class="wrapper w-full">
          <p class="font-bold text-[5.6em] uppercase tracking-wider">
            hi!, there
          </p>
          <p class="font-bold text-[5.6em] uppercase tracking-wider">
            welcome to my page
          </p>
        </div>
      </div>

      <!-- Footer dengan Marquee -->
      <div
        class="wrapper-footer flex items-center justify-center w-full border-t border-gray-700 h-[250px] overflow-hidden relative"
      >
        <div class="absolute top-[calc(40vh-350px)]">
          <div ref="slider" class="relative whitespace-nowrap">
            <p ref="firstText" class="relative m-0 text-[#dadada] text-[8em]">
              Web Developer - React Js - Next Js - Vue Js - Nuxt Js - Laravel -
            </p>
            <p
              ref="secondText"
              class="absolute left-full top-0 m-0 text-[#dadada] text-[8em]"
            >
              Web Developer - React Js - Next Js - Vue Js - Nuxt Js - Laravel -
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
