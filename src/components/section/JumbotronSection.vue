<script setup>
import { ref, onMounted } from "vue";
import { useGsap } from "#gsap";

const gsap = useGsap();


const firstText = ref(null);
const secondText = ref(null);
const slider = ref(null);

const textContent = ref("there");
const texts = ["there", "I'm Dady Bima"];

const typewriterText = ref(null);
const cursor = ref(null);

let currentIndex = 0;
let xPercent = 0;
let direction = -1;

// animated typing
const animateTyping = () => {
  gsap.fromTo(
    typewriterText.value,
    { width: "0px" },
    {
      width: "auto",
      duration: 0.5,
      ease: "steps(20)",
      onComplete: () => {
        setTimeout(() => {
          gsap.to(typewriterText.value, {
            width: "0px",
            duration: 0.8,
            ease: "steps(15)",
            onComplete: () => {
              currentIndex = (currentIndex + 1) % texts.length;
              textContent.value = texts[currentIndex];
              animateTyping();
            },
          });
        }, 2000);
      },
    }
  );
};

// animated marquee
const animate = () => {
  if (xPercent < -100) {
    xPercent = 0;
  } else if (xPercent > 0) {
    xPercent = -100;
  }
  gsap.set(firstText.value, { xPercent });
  gsap.set(secondText.value, { xPercent });
  requestAnimationFrame(animate);
  xPercent += 0.08 * direction;
};

onMounted(() => {
  gsap.registerPlugin(ScrollTrigger);
  animateTyping();

  gsap.to(cursor.value, {
    opacity: 0,
    repeat: -1,
    yoyo: true,
    duration: 0.5,
    ease: "power1.inOut",
  });

  gsap.to(typewriterText.value, {
    borderRightColor: "transparent",
    repeat: -1,
    yoyo: true,
    duration: 0.5,
    ease: "power1.inOut",
  });

  // Animasi Marquee
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
  <div id="home" class="min-h-screen bg-black p-24">
    <div
      class="flex flex-col items-center justify-between border-2 border-gray-700 rounded-xl h-[760px] w-full"
    >
      <!-- Header -->
      <div
        class="wrapper-header pattern-stripes rounded-t-[10px] text-[#dedede] px-10 w-full h-[520px] flex items-center justify-center text-2xl relative"
      >
        <div class="typewriter wrapper w-full relative z-10">
          <div
            class="font-bold text-[5.6em] uppercase tracking-wider flex items-center mx-auto"
          >
            hi!,&nbsp;
            <span
              ref="typewriterText"
              class="border-r-[5px] border-white whitespace-nowrap overflow-hidden inline-block"
            >
              {{ textContent }}
            </span>
            <span ref="cursor" class="">&nbsp;</span>
          </div>
          <p class="font-bold text-[5.6em] uppercase tracking-wider">
            welcome to my page
          </p>
        </div>
        <div
          class="absolute z-0 h-full w-full bg-[repeating-linear-gradient(45deg,_#333_0px,_#666_10px,_transparent_45px,_transparent_30px)] rounded-t-[10px]"
        ></div>
      </div>

      <!-- Footer dengan Marquee -->
      <div
        class="wrapper-footer flex items-center justify-center w-full border-t border-gray-700 h-[250px] overflow-hidden relative"
      >
        <div class="absolute top-[calc(40vh-350px)]">
          <div ref="slider" class="relative whitespace-nowrap font-semibold">
            <p ref="firstText" class="relative m-0 text-[#dadada] text-[8em]">
              Web Developer - React Js - Next Js - Vue Js - Nuxt Js - Laravel -
            </p>
            <p
              ref="secondText"
              class="absolute left-full top-0 m-0 text-[#dadada] text-[8em]"
            >
               Web Developer - React Js - Next Js - Vue Js - Nuxt Js - Laravel
              -
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
