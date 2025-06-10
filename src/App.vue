<script>
import Header from '@/components/Header.vue';
import Skill from '@/components/Skill.vue';
import SocialLink from '@/components/SocialLink.vue';
import sections from '@/data/sections.json';
import Certificates from '@/components/Certificates.vue';
import ContactMe from '@/components/ContactMe.vue';
import Education from '@/components/Education.vue';
import educations from '@/data/education.json'
import AboutMe from '@/components/AboutMe.vue';


export default {
  components: {
    Header,
    Skill,
    SocialLink,
    Certificates,
    ContactMe,
    Education,
    AboutMe,
  },
  data() {
    return {
      activeNav: 'about',
      isDarkMode: true,
      isMobileMenuOpen: false,
      sections,
      educations,
    }
  },
  computed: {
    backgroundColor() {
      return this.isDarkMode ? 'bg-gray-900' : 'bg-gray-100';
    },
    textColor() {
      return this.isDarkMode ? 'text-white' : 'text-black';
    },
    modeImg() {
      return this.isDarkMode
        ? "https://cdn-icons-png.flaticon.com/128/17648/17648604.png"
        : "https://cdn-icons-png.flaticon.com/128/12301/12301351.png";
    }
  },
  methods: {
    setActive(section) {
      this.activeNav = section;
      this.isMobileMenuOpen = false;
      this.scrollToSection(`#${section}`);
    },
    scrollToSection(id) {
      this.$nextTick(() => {
        const section = document.querySelector(id);
        if (section) {
          section.scrollIntoView({ behavior: 'smooth' });
        }
      });
    },
    toggleMode() {
      this.isDarkMode = !this.isDarkMode;
    },
    toggleMenu() {
      this.isMobileMenuOpen = !this.isMobileMenuOpen;
    },
  }
}
</script>

<template>
  <div :class="[backgroundColor, textColor]" class="min-h-screen overflow-x-hidden">
    <Header
      :active-nav="activeNav"
      :is-dark-mode="isDarkMode"
      :is-mobile-menu-open="isMobileMenuOpen"
      :mode-img="modeImg"
      @set-active="setActive"
      @toggle-mode="toggleMode"
      @toggle-menu="toggleMenu"
    />

    <section class="min-h-screen flex flex-col-reverse md:flex-row items-center justify-center px-6 gap-12 md:gap-52 z-10">
      <div>
        <h1 class="text-4xl md:text-5xl font-bold leading-snug text-center md:text-left animate__animated animate__jackInTheBox">
          Hi,<br>
          I'm <span class="text-teal-700 font-semibold">Lester</span><br>
          Aspiring Web Developer
        </h1>
        <div class="flex justify-center item-center mt-16">
          <button
            @click="setActive('contact')" :active="activeNav === 'contact'"
            class="inline-flex items-center rounded-md border border-transparent bg-gray-700 px-4 py-2 text-xs font-semibold uppercase tracking-widest text-white transition duration-150 ease-in-out hover:bg-teal-900">
            Contact me
          </button>
        </div>
              
        <div class="mt-16 flex justify-center items-center space-x-6 animate__animated animate__slideInUp">
          <SocialLink src="https://cdn-icons-png.flaticon.com/128/4494/4494497.png" alt="LinkedIn" link="https://www.linkedin.com/in/jlhebres/"></SocialLink>
          <SocialLink src="https://cdn-icons-png.flaticon.com/128/5968/5968764.png" alt="Facebook" link="https://www.facebook.com/jl.hebres1"></SocialLink>
          <SocialLink src="https://cdn-icons-png.flaticon.com/128/5968/5968896.png" alt="GitHub" link="https://github.com/resuta17"></SocialLink>
        </div>
      </div>
    </section>
    
    <section id="about" class="mt-10 px-4">
      <AboutMe/>
    </section>
    
    <section id="experience" class="mt-36 m-5">
      <div class="text-center text-xl font-semibold mb-16 text-teal-700">
        <p>Experience</p>
        <hr class="border-t-2 border-teal-700 mt-2 w-24 mx-auto" />
      </div>
      <div class="flex justify-center">
        <div
          class="flex items-start space-x-4 max-w-4xl w-full px-4 border border-teal-700 rounded-xl p-6 shadow-lg">
          <div class="w-20 flex justify-center">
            <img :src="'https://media.licdn.com/dms/image/v2/D560BAQEeJkkTZrZb8A/company-logo_200_200/company-logo_200_200/0/1704273708397?e=1753315200&v=beta&t=QzK7HH73jp-GElxDH6VSiASxXIZrbI1InnQwIktOUR4'"
              title="phCollab Logo" class="w-16 h-16 flex-shrink-0">
          </div>

          <div>
            <p class="text-base font-semibold">phCollab - Internship</p>
            <p class="text-gray-500 font-semibold">Feb 2025 - May 2025</p>
            <p class="text-sm leading-relaxed">
              I completed my internship at phCollab as part of my
              Bachelor's degree requirement, where
              I gained hands-on experience in Quality Assurance (QA), test automation, and
              frontend development.
            </p>
          </div>
        </div>
      </div>
    </section>
    
    <section id="education" class="mt-36 m-5">
      <div class="text-center text-xl font-semibold mb-16 text-teal-700">
        <p>Education</p>
        <hr class="border-t-2 border-teal-700 mt-2 w-24 mx-auto" />
      </div>
      <Education v-for="education in educations"
        :image = "education.image"
        :title = "education.title" 
        :schoolLink = "education.schoolLink"
        :degree ="education.degree"
        :schoolYear = "education.schoolYear"
      > 
        {{ education.description }}
      </Education>
      
    </section>
    
    <section id="certification" class="mt-36">
        <Certificates v-bind:darkMode = "isDarkMode"></Certificates>
    </section>
    

    <section id="Skills" class="mt-36">
      <div class="text-center text-xl font-semibold mb-20 text-teal-700">
        <p>Skills</p>
        <hr class="border-t-2 border-teal-700 mt-2 w-12 mx-auto"/> 
      </div>
      <div class="flex justify-center items-center">
        <ul class="grid grid-cols-2 gap-x-4 gap-y-3 sm:gap-x-20 sm:gap-y-4 md:gap-x-40 md:gap-y-5 list-none text-xl">
          <li><Skill :icon="'https://cdn-icons-png.flaticon.com/128/1051/1051277.png'">HTML</Skill></li>
          <li><Skill :icon="'https://cdn-icons-png.flaticon.com/128/5968/5968292.png'">JavaScript</Skill></li>
          <li><Skill :icon="'https://cdn-icons-png.flaticon.com/128/732/732190.png'">CSS</Skill></li>
          <li><Skill :icon="'https://cdn-icons-png.flaticon.com/128/919/919830.png'">PHP</Skill></li>
          <li><Skill :icon="'https://cdn-icons-png.flaticon.com/128/6132/6132221.png'">C#</Skill></li>
          <li><Skill :icon="'https://cdn-icons-png.flaticon.com/128/16845/16845837.png'">MySQL</Skill></li>
          <li><Skill :icon="'https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/1184px-Vue.js_Logo_2.svg.png'">Vue.js</Skill></li>
          <li><Skill :icon="'https://download.logo.wine/logo/Laravel/Laravel-Logo.wine.png'">Laravel</Skill></li>
          <li><Skill :icon="'https://cdn-icons-png.flaticon.com/128/4494/4494740.png'">Git</Skill></li>
          <li><Skill :icon="'https://pngimg.com/d/linux_PNG27.png'">Linux</Skill></li>
        </ul>
      </div>
    </section>
    
    <section id="Projects" class="mt-36">
      <div class="text-center text-xl font-semibold mb-4 text-teal-700">
        <p>Projects</p>
        <hr class="border-t-2 border-teal-700 mt-2 w-24 mx-auto" />
      </div>
    </section>
    
    <section id="contact" class="mt-36 bg-teal-900 p-6">
      <ContactMe></ContactMe>
      <div class="mt-16 flex justify-center items-center space-x-6 animate__animated animate__slideInUp">
        <SocialLink src="https://cdn-icons-png.flaticon.com/128/4494/4494497.png" alt="LinkedIn" link="https://www.linkedin.com/in/jlhebres/"></SocialLink>
        <SocialLink src="https://cdn-icons-png.flaticon.com/128/5968/5968764.png" alt="Facebook" link="https://www.facebook.com/jl.hebres1"></SocialLink>
        <SocialLink src="https://cdn-icons-png.flaticon.com/128/5968/5968896.png" alt="GitHub" link="https://github.com/resuta17"></SocialLink>
      </div>
    </section>      
  </div>
</template>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>