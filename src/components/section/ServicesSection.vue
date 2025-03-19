<template>
  <div
  id="services"
    class="horizontal flex overflow-x-hidden min-h-screen bg-black text-white"
  >
    <!-- Hero Section -->
    <section
      class="content container relative mx-auto px-4 py-20 md:py-32 min-h-screen min-w-screen w-full flex flex-col justify-center items-center"
    >
      <div class="container mx-auto">
        <div
          class="mx-auto flex items-center border border-gray-700 rounded-[10px]"
        >
          <p
            class="w-6/12 text-3xl text-white border-r border-gray-700 p-10 text-left leading-[150%] tracking-wide"
          >
            We specialize in transforming ideas into impactful digital
            experiences. By leveraging cutting-edge technologies and creative
            strategies, we help brands and individuals thrive in a competitive
            landscape. Discover our projects and let's build something
            extraordinary together.
          </p>
          <p
            class="text-6xl w-6/12 capitalize border border-gray-700 text-left leading-[120%] p-10 font-semibold mb-6 bg-gradient-to-r from-blue-400 to-purple-600 bg-clip-text text-transparent"
          >
            empowering your vision, crafting your success
          </p>
        </div>
        <p
          class="flex relative top-40 justify-center w-full text-xl capitalize font-thin italic text-gray-400"
        >
          keep scrolling
        </p>
      </div>
    </section>

    <!-- Portfolio Section with Large Cards -->
    <section
      v-for="project in projects"
      :key="project.id"
      ref="projectCards"
      class="content container mx-auto px-4 py-16 min-h-screen min-w-screen flex items-center"
    >
      <div class="container mx-auto">
        <div
          class="bg-gray-900/60 border border-gray-700 rounded-xl overflow-hidden"
        >
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
            <!-- Project Image -->
            <div class="relative h-[300px] lg:h-[500px] overflow-hidden">
              <img
                :src="project.image"
                :alt="project.title"
                class="w-full h-full object-cover"
              />
            </div>

            <!-- Project Details -->
            <div class="p-8 flex flex-col justify-center">

              <div class="p-8 flex flex-col justify-center">
                <h2 class="text-3xl md:text-4xl font-bold mb-4">
                  {{ project.title }}
                </h2>

                <p class="text-gray-300 text-lg mb-6">
                  {{ project.description }}
                </p>

                <div class="mb-8">
                  <h3 class="text-xl font-semibold mb-3">Technologies Used:</h3>
                  <div class="flex flex-wrap gap-3">
                    <span
                      v-for="framework in project.frameworks"
                      :key="framework"
                      class="px-4 py-2 bg-gray-800 rounded-full text-sm font-medium"
                    >
                      {{ framework }}
                    </span>
                  </div>
                </div>

                <button
                  class="w-fit px-4 py-2 border border-white/20 rounded-md hover:bg-white/10 flex items-center group"
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
      </div>
    </section>

    <!-- CTA Section -->
    <section class="content bg-black min-w-screen min-h-screen px-4 py-20 ">
      <div class="mx-auto container">
        <div
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
import { ref, onMounted } from "vue";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const projects = ref([
  {
    id: 1,
    title: "E-commerce Platform",
    description:
      "A comprehensive e-commerce solution with advanced product filtering, user authentication, and a seamless checkout process. This platform was built with performance and scalability in mind, ensuring a smooth shopping experience for customers across all devices.",
    image:
      "https://via.placeholder.com/800x600/333/666?text=E-commerce+Platform",
    frameworks: ["Vue.js", "Nuxt.js", "Tailwind CSS", "Stripe", "MongoDB"],
  },
  {
    id: 2,
    title: "Corporate Dashboard",
    description:
      "An intuitive dashboard for a financial services company that visualizes complex data in an accessible way. The dashboard includes real-time analytics, customizable reports, and role-based access control to ensure data security.",
    image:
      "https://via.placeholder.com/800x600/333/666?text=Corporate+Dashboard",
    frameworks: ["Vue.js", "D3.js", "Express", "PostgreSQL", "Docker"],
  },
  {
    id: 3,
    title: "Mobile Fitness App",
    description:
      "A cross-platform fitness application that helps users track their workouts, set goals, and connect with friends. The app includes features like workout plans, progress tracking, and social sharing to keep users motivated.",
    image: "https://via.placeholder.com/800x600/333/666?text=Fitness+App",
    frameworks: ["Vue Native", "Firebase", "Vuex", "Node.js", "GraphQL"],
  },
  {
    id: 4,
    title: "Educational Platform",
    description:
      "An interactive learning platform for students and educators featuring course management, video lectures, quizzes, and progress tracking. The platform supports multiple learning formats and provides detailed analytics for educators.",
    image:
      "https://via.placeholder.com/800x600/333/666?text=Educational+Platform",
    frameworks: ["Vue.js", "TypeScript", "Django", "AWS", "Socket.io"],
  },
  {
    id: 5,
    title: "Real Estate Marketplace",
    description:
      "A comprehensive real estate platform that connects buyers, sellers, and agents. Features include property listings, advanced search filters, virtual tours, and appointment scheduling. The platform uses AI to provide personalized property recommendations.",
    image:
      "https://via.placeholder.com/800x600/333/666?text=Real+Estate+Marketplace",
    frameworks: ["Nuxt.js", "Prisma", "PostgreSQL", "Mapbox", "Vercel"],
  },
]);

const projectCards = ref([]);

onMounted(() => {
  gsap.to(".horizontal .content", {
      x: () => -(projectCards.value.length + 1) * window.innerWidth,
      ease: "none",
      scrollTrigger: {
        trigger: ".horizontal",
        pin: true,
        scrub: 1,
        end: () => "+=" + document.querySelector(".horizontal").offsetWidth,
      },
    });

  setTimeout(async () => {

    projectCards.value.forEach((card, index) => {
      gsap.fromTo(
        card,
        { x: 100, opacity: 0 },
        {
          y: 0,
          opacity: 1,
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
  }, 100);
});
</script>

<style scope>
.horizontal .content {
  display: grid;
  place-items: center;
  flex-shrink: 0;
}
</style>
