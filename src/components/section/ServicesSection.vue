<template>
  <div
    id="services"
    class="horizontal flex overflow-x-hidden min-h-screen bg-black text-white"
  >
    <!-- Hero Section -->
    <section
      id="hero"
      class="content container relative mx-auto px-4 py-20 md:py-32 min-h-screen min-w-screen w-full flex flex-col justify-center items-center"
    >
      <div class="container mx-auto">
        <div
          id="heroServices"
          class="mx-auto flex items-center border border-gray-700 rounded-[10px]"
        >
          <p
            id="heroServicesDesc"
            class="w-6/12 text-3xl text-white border-r border-gray-700 p-10 text-left leading-[150%] tracking-wide"
          >
            We specialize in transforming ideas into impactful digital
            experiences. By leveraging cutting-edge technologies and creative
            strategies, we help brands and individuals thrive in a competitive
            landscape. Discover our projects and let's build something
            extraordinary together.
          </p>
          <p
            id="heroServicesTitle"
            class="text-6xl w-6/12 capitalize border border-gray-700 text-left leading-[120%] p-10 font-semibold mb-6 bg-gradient-to-r from-blue-400 to-purple-600 bg-clip-text text-transparent"
          >
            empowering your vision, crafting your success
          </p>
        </div>
        <p
          id="heroServicesScroll"
          class="flex relative top-40 justify-center w-full text-xl capitalize font-thin italic text-gray-400"
        >
          keep scrolling
        </p>
      </div>
    </section>

    <!-- Portfolio Section with Large Cards -->
    <section
      id="projects"
      v-for="(project, index) in data"
      :key="index"
      ref="projectCards"
      class="content container mx-auto px-4 py-16 min-w-screen min-h-screen flex items-center"
    >
      <div class="container mx-auto">
        <div
          class="bg-gray-900/60 border border-gray-700 rounded-xl overflow-hidden"
        >
          <div id="projectCard" class="grid grid-cols-1 lg:grid-cols-2 gap-8">
            <!-- Project Image -->
            <div
              id="imgCard"
              class="relative h-[300px] lg:h-[500px] overflow-hidden"
            >
              <img
                v-if="project.img"
                :src="project.img"
                :alt="project.title || 'Project Image'"
                class="w-full h-full object-cover"
              />

              <div
                v-else
                class="flex items-center justify-center w-full h-full bg-gray-800 text-white"
              >
                No Image Available
              </div>
            </div>

            <!-- Project Details -->
            <div id="detailsCard" class="p-8 flex flex-col justify-center">
              <h2 class="text-3xl md:text-4xl font-bold mb-4">
                {{ project.title }}
              </h2>
              <p class="text-gray-300 text-lg mb-6">{{ project.desc }}</p>
              <div class="mb-8 framework">
                <h3 class="text-xl font-semibold mb-3">Technologies Used:</h3>
                <div class="flex flex-wrap gap-3">
                  <span
                    v-if="project.framework"
                    class="px-4 py-2 bg-gray-800 rounded-full text-sm font-medium"
                  >
                    {{ project.framework }}
                  </span>
                </div>
              </div>
              <button
                class="w-fit px-4 py-2 border cursor-pointer border-white/20 rounded-md hover:bg-white/10 flex items-center group"
              >
                View Project Details
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="ml-2 h-4 w-4 transition-transform group-hover:translate-x-1"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M14 5l7 7m0 0l-7 7m7-7H3"
                  />
                </svg>
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section
      id="cta"
      class="content bg-black min-w-screen min-h-screen px-4 py-20"
    >
      <div class="mx-auto container">
        <div
          id="ctaContent"
          class="bg-gradient-to-r from-blue-900/50 to-purple-900/50 p-12 rounded-2xl text-center border-2 border-gray-700"
        >
          <h2 class="text-3xl md:text-4xl font-bold mb-6">
            Ready to start your project?
          </h2>
          <p class="text-xl text-gray-300 mb-8 max-w-2xl mx-auto">
            Let's create something amazing together. Contact us today to discuss
            your ideas.
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <button
              class="px-6 py-3 rounded-md bg-white text-black hover:bg-gray-200 font-medium"
            >
              Get a Free Quote
            </button>
            <button
              class="px-6 py-3 rounded-md border border-white text-white hover:bg-white/10 font-medium"
            >
              View Our Process
            </button>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from "vue";
import axios from "axios";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

if (typeof window !== "undefined") {
  gsap.registerPlugin(ScrollTrigger);
}

const fetchData = async () => {
  try {
    const response = await axios.get("http://127.0.0.1:8000/api/services");
    data.value = response.data ?? [];
    console.log("Fetched Data:", data.value);
    await nextTick();

    if (widthMobile.value > 375) {
      animateProjects();
    } else {
      animateProjectsMobile();
    }
  } catch (error) {
    console.error("Error fetching data:", error.response?.data || error.message);
  }
};

const data = ref([]);
const projectCards = ref([]);
const widthMobile = ref(typeof window !== "undefined" ? window.innerWidth : 0);

const handleResize = () => {
  widthMobile.value = window.innerWidth;

  // Clear existing ScrollTrigger instances
  ScrollTrigger.getAll().forEach(trigger => trigger.kill());

  // Re-initialize animations based on screen size
  if (widthMobile.value > 375) {
    nextTick(() => animateProjects());
  } else {
    nextTick(() => animateProjectsMobile());
  }
};


const animateProjects = () => {
  gsap.to(".horizontal .content", {
    x: () => -(projectCards.value.length + 1) * window.innerWidth,
    ease: "none",
    scrollTrigger: {
      trigger: ".horizontal",
      pin: true,
      scrub: 1,
      end: () => "+=" + (document.querySelector(".horizontal")?.offsetWidth || 0),
    },
  });

  projectCards.value.forEach((card, index) => {
    gsap.fromTo(
      card,
      { opacity: 0, x: 100 },
      {
        opacity: 1,
        x: 0,
        duration: 1,
        ease: "power3.out",
        scrollTrigger: {
          trigger: card,
          start: "top 80%",
          toggleActions: "play none none none",
        },
        delay: 0.2 * index,
      }
    );
  });
};

const animateProjectsMobile = () => {
  projectCards.value.forEach((card) => {
    gsap.fromTo(
      card,
      { opacity: 0, y: 50 },
      {
        opacity: 1,
        y: 0,
        duration: 0.8,
        ease: "power2.out",
        scrollTrigger: {
          trigger: card,
          start: "top 90%",
          toggleActions: "play none none none",
        },
      }
    );
  });
};

onMounted(() => {
  console.log("Width Mobile:", widthMobile.value);

  // Add resize listener
  window.addEventListener('resize', handleResize);

  // Fetch data and initialize animations
  fetchData();

  // Clean up
  return () => {
    window.removeEventListener('resize', handleResize);
    ScrollTrigger.getAll().forEach(trigger => trigger.kill());
  };
});
</script>

<style scoped>
.horizontal .content {
  display: grid;
  place-items: center;
  flex-shrink: 0;
}

/* Ensure text gradient works */
.bg-clip-text {
  -webkit-background-clip: text;
  background-clip: text;
}

@media (max-width: 375px) {
  /* Global structure changes */
  #services {
    display: block;
    height: auto;
    overflow-x: visible;
    overflow-y: auto;
  }

  .horizontal {
    display: block;
  }

  .horizontal .content {
    display: block;
    min-width: auto;
    min-height: auto;
    width: 100%;
    height: auto;
    transform: none !important; /* Prevent GSAP horizontal scrolling on mobile */
  }

  /* Hero section */
  #hero {
    padding: 2rem 1rem;
    height: auto;
    min-height: auto;
  }

  #heroServices {
    flex-direction: column-reverse;
    margin: 0;
    border-width: 1px;
  }

  #heroServicesTitle {
    width: 100%;
    font-size: 2rem;
    padding: 1rem;
    border-bottom: 1px solid #4B5563;
    border-right: none;
    border-left: none;
    border-top: none;
    margin-bottom: 0;
    line-height: 1.2;
  }

  #heroServicesDesc {
    width: 100%;
    padding: 1rem;
    font-size: 1rem;
    border-right: none;
    line-height: 1.5;
  }

  #heroServicesScroll {
    display: none;
  }

  /* Project sections */
  #projects {
    padding: 2rem 1rem;
    height: auto;
    min-height: auto;
    margin-bottom: 2rem;
  }

  #projectCard {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  #imgCard {
    height: 200px;
  }

  #detailsCard {
    padding: 1rem;
  }

  #detailsCard h2 {
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
  }

  #detailsCard p {
    font-size: 0.875rem;
    margin-bottom: 0.75rem;
    line-height: 1.4;
  }

  .framework {
    margin-bottom: 1rem;
  }

  .framework h3 {
    font-size: 1rem;
    margin-bottom: 0.5rem;
  }

  .framework div span {
    font-size: 0.75rem;
    padding: 0.25rem 0.75rem;
  }

  #detailsCard button {
    font-size: 0.75rem;
    padding: 0.5rem 0.75rem;
  }

  #detailsCard button svg {
    width: 0.75rem;
    height: 0.75rem;
  }

  /* CTA section */
  #cta {
    padding: 2rem 1rem;
    height: auto;
    min-height: auto;
  }

  #ctaContent {
    padding: 1.5rem 1rem;
    width: 100%;
    margin: 0 auto;
  }

  #ctaContent h2 {
    font-size: 1.2rem;
    margin-bottom: 0.75rem;
  }

  #ctaContent p {
    font-size: 0.875rem;
    margin-bottom: 1rem;
  }

  #ctaContent div {
    gap: 0.5rem;
  }

  #ctaContent div button {
    font-size: 0.75rem;
    padding: 0.5rem 0.75rem;
  }
}
</style>