<script>
import NavLink from '@/components/NavLink.vue';
import Swal from 'sweetalert2';

export default {
  components: {
    NavLink
  },
  data() {
    return {
      activeNav: 'about',
      isDarkMode: true,
      isMobileMenuOpen: false,
      currentCert: 0,
      certificates: [
        {
          title: 'Introduction to Git and GitHub',
          img: 'https://s3.amazonaws.com/coursera_assets/meta_images/generated/CERTIFICATE_LANDING_PAGE/CERTIFICATE_LANDING_PAGE~X35RFUDR4XBT/CERTIFICATE_LANDING_PAGE~X35RFUDR4XBT.jpeg',
          issued: 'May 2024',
          id: 'X35RFUDR4XBT',
          link: 'https://www.coursera.org/account/accomplishments/verify/X35RFUDR4XBT',
        }, {
          title: 'Google IT Support',
          img: 'https://s3.amazonaws.com/coursera_assets/meta_images/generated/CERTIFICATE_LANDING_PAGE/CERTIFICATE_LANDING_PAGE~RK9DHP48APNR/CERTIFICATE_LANDING_PAGE~RK9DHP48APNR.jpeg',
          issued: 'Jun 2024',
          id: 'RK9DHP48APNR',
          link: 'https://www.coursera.org/account/accomplishments/specialization/RK9DHP48APNR',
        }, {
          title: 'Google IT Automation with Python',
          img: 'https://s3.amazonaws.com/coursera_assets/meta_images/generated/CERTIFICATE_LANDING_PAGE/CERTIFICATE_LANDING_PAGE~GGS5N7QWE7FV/CERTIFICATE_LANDING_PAGE~GGS5N7QWE7FV.jpeg',
          issued: 'May 2024',
          id: 'GGS5N7QWE7FV',
          link: 'https://www.coursera.org/account/accomplishments/specialization/GGS5N7QWE7FV',
        }, {
          title: 'Troubleshooting and Debugging Techniques',
          img: 'https://s3.amazonaws.com/coursera_assets/meta_images/generated/CERTIFICATE_LANDING_PAGE/CERTIFICATE_LANDING_PAGE~5ZQHTK6MSB49/CERTIFICATE_LANDING_PAGE~5ZQHTK6MSB49.jpeg',
          issued: 'May 2024',
          id: '5ZQHTK6MSB49',
          link: 'https://www.coursera.org/account/accomplishments/verify/5ZQHTK6MSB49',
        }, {
          title: 'Technical Support Fundamentals',
          img: 'https://s3.amazonaws.com/coursera_assets/meta_images/generated/CERTIFICATE_LANDING_PAGE/CERTIFICATE_LANDING_PAGE~META6P6YPNEV/CERTIFICATE_LANDING_PAGE~META6P6YPNEV.jpeg',
          issued: 'May 2024',
          id: 'META6P6YPNEV',
          link: 'https://www.coursera.org/account/accomplishments/verify/META6P6YPNEV',
        },
      ]
    }
  },
  computed: {
    backgroundColor() {
      return this.isDarkMode ? 'bg-gray-900' : 'bg-white';
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
    flash(message) {
      Swal.fire("Success!", message, 'success');
    },
    nextCert() {
      this.currentCert = (this.currentCert + 1) % this.certificates.length;
    },
    prevCert() {
      this.currentCert = (this.currentCert - 1 + this.certificates.length) % this.certificates.length;
    }
  }
}
</script>

<template>
  <div :class="[backgroundColor, textColor]" class="min-h-screen overflow-x-hidden">
    <!-- Header -->
    <header class="bg-teal-900 shadow h-16 flex justify-between items-center px-4 sticky top-0 z-50">
      <div class="ml-2 md:ml-8 flex items-center space-x-2">
        <div>
          <h1 class="text-white font-bold text-base md:text-lg">
            John Lester H. Hebres
          </h1>
          <p class="text-white text-xs md:text-sm">
            BS Computer Science Graduate
          </p>
        </div>
      </div>

      <button @click="toggleMenu" class="md:hidden text-white focus:outline-none">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>

      <nav class="hidden md:flex flex-wrap items-center justify-end space-x-2 md:space-x-4 mr-4">
        <NavLink @click="setActive('about')"  :active="activeNav === 'about'" class="text-white">
          About Me
        </NavLink>
        <NavLink @click="setActive('experience')" :active="activeNav === 'experience'" class="text-white">
          Experience
        </NavLink>
        <NavLink @click="setActive('education')" :active="activeNav === 'education'" class="text-white">
          Education
        </NavLink>
        <NavLink @click="setActive('certification')"  :active="activeNav === 'certification'" class="text-white">
          Certificates
        </NavLink>
        <NavLink @click="setActive('Skills')"  :active="activeNav === 'Skills'" class="text-white">
          Skills
        </NavLink>
        <NavLink @click="setActive('Projects')":active="activeNav === 'Projects'" class="text-white">
          Projects
        </NavLink>
        <img :src="modeImg" title="light dark icons" class="w-8 h-8 cursor-pointer" @click="toggleMode" />
      </nav>

      <transition name="fade">
        <div v-if="isMobileMenuOpen" class="absolute top-16 left-0 w-full bg-teal-900 flex flex-col items-start px-4 py-4 space-y-2 md:hidden z-40">
          <NavLink @click="setActive('about')" :active="activeNav === 'about'" class="text-white w-full">
            About Me
          </NavLink>
          <NavLink @click="setActive('experience')"  :active="activeNav === 'experience'" class="text-white w-full">
            Experience
          </NavLink>
          <NavLink @click="setActive('education')"  :active="activeNav === 'education'" class="text-white w-full">
            Education
          </NavLink>
          <NavLink @click="setActive('certification')":active="activeNav === 'certification'" class="text-white w-full">
            Certificates
          </NavLink>
          <NavLink @click="setActive('Skills')" :active="activeNav === 'Skills'" class="text-white w-full">
            Skills
          </NavLink>
          <NavLink @click="setActive('Projects')" href="#Projects" :active="activeNav === 'Projects'" class="text-white w-full">
            Projects
          </NavLink>
          <img :src="modeImg" title="light dark icons" class="w-8 h-8 mt-2 cursor-pointer" @click="toggleMode" />
        </div>
      </transition>
    </header>

      <section id="about" class="min-h-screen flex flex-col-reverse md:flex-row items-center justify-center px-6 gap-12 md:gap-52 z-10">
        <div>
          <h1 class="text-4xl md:text-5xl font-bold leading-snug text-center md:text-left">
            Hi,<br>
            I'm <span class="text-teal-700 font-semibold">Lester</span><br>
            Aspiring Web Developer
          </h1>
          <div class="flex justify-center item-center mt-16">
            <button
              @click="flash('Test Message')"
              class="inline-flex items-center rounded-md border border-transparent bg-gray-700 px-4 py-2 text-xs font-semibold uppercase tracking-widest text-white transition duration-150 ease-in-out hover:bg-teal-900">
              Contact me
            </button>
          </div>
          
          <div class="mt-16 flex justify-center items-center space-x-6">
            <a href="https://www.linkedin.com/in/jlhebres/" target="_blank" class="w-10 h-10 flex items-center justify-center">
              <img
                src="https://cdn-icons-png.flaticon.com/128/4494/4494497.png"
                alt="LinkedIn"
                class="w-8 h-8 transform transition-transform duration-200 hover:scale-125"
              />
            </a>

            <a href="https://www.facebook.com/jl.hebres1" target="_blank" class="w-10 h-10 flex items-center justify-center">
              <img
                src="https://cdn-icons-png.flaticon.com/128/5968/5968764.png"
                alt="Facebook"
                class="w-8 h-8 transform transition-transform duration-200 hover:scale-125"
              />
            </a>

            <a href="https://github.com/resuta17" target="_blank" class="w-10 h-10 flex items-center justify-center">
              <img
                src="https://cdn-icons-png.flaticon.com/128/5968/5968896.png"
                alt="GitHub"
                class="w-8 h-8 transform transition-transform duration-200 hover:scale-125"
              />
            </a>
          </div>
        </div>
      </section>
      
      <section id="about" class="mt-10 px-4">
                <div class="text-center text-xl font-semibold mb-10 text-teal-700">
                    <p>About me</p>
                    <hr class="border-t-2 border-teal-700 mt-2 w-24 mx-auto" />
                </div>

                <div class="max-w-4xl mx-auto flex flex-col md:flex-row items-center md:items-start gap-6 md:gap-12">
                    <div class="flex-shrink-0">
                    <img
                        :src="`https://media.licdn.com/dms/image/v2/D5603AQFGn1dlumaH5A/profile-displayphoto-shrink_400_400/B56ZbicFj_H4Ao-/0/1747555736915?e=1755129600&v=beta&t=Rxgns4gM_TSoDxiic5zoDep5CCQPuQqy86ntOKRmiyM`"
                        alt="Profile Picture"
                        class="w-40 h-40 sm:w-48 sm:h-48 md:w-56 md:h-56 object-cover rounded-full mx-auto md:mx-0"
                    />
                    </div>

                    <div class="text-center md:text-left">
                    <p class="text-base sm:text-lg leading-relaxed">
                        I'm <strong>John Lester Hababag Hebres</strong>, a <em>BSCS cum laude</em> graduate with
                        a strong interest in web development. I'm currently focusing on learning and building
                        projects with <strong>Laravel</strong> and <strong>Vue.js</strong> to sharpen my skills in
                        full-stack development.
                    </p>

                    <div class="flex justify-center mt-6">
                        <button
                        class="inline-flex items-center rounded-md border border-transparent bg-gray-700 px-4 py-2 text-xs font-semibold uppercase tracking-widest text-white transition duration-150 ease-in-out hover:bg-teal-900"
                        >
                        Download CV
                        </button>
                    </div>
                    </div>
                </div>
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

                <div class="flex justify-center mb-4">
                    <div
                        class="flex items-start space-x-4 max-w-4xl w-full px-4 border border-teal-700 rounded-xl p-6 shadow-lg">
                        <div class="w-20 flex justify-center items-start">
                            <img :src="'https://www.ccdisorsogon.edu.ph/wp-content/uploads/2018/04/cropped-ccdilogo.png'"
                                title="CCDI Sorsogon" class="w-16 h-16 flex-shrink-0">
                        </div>
                        <div>
                            <a href="https://www.ccdisorsogon.edu.ph/" target="_blank" class="text-base font-semibold">
                                Computer Communication Development Institute - Sorsogon City
                            </a>
                            <p class="text-sm">Bachelor of Science in Computer Science</p>
                            <p class="text-gray-500 font-semibold">2021 - 2025</p>
                        </div>
                    </div>
                </div>
                
                <div class="flex justify-center">
                    <div
                        class="flex items-start space-x-4 max-w-4xl w-full px-4 border border-teal-700 rounded-xl p-6 shadow-lg">
                        <div class="w-20 flex justify-center items-start">
                            <img :src="'https://www.ccdisorsogon.edu.ph/wp-content/uploads/2018/04/cropped-ccdilogo.png'"
                                title="CCDI SHS" class="w-16 h-16 flex-shrink-0">
                        </div>
                        <div>
                            <a href="https://www.ccdisorsogon.edu.ph/" target="_blank" class="text-base font-semibold">
                                Computer Communication Development Institute SHS - Sorsogon City
                            </a>
                            <p class="text-sm">TVL-ICT Programming NC IV</p>
                            <p class="text-gray-500 font-semibold">2019 - 2021</p>
                        </div>
                    </div>
                </div>
            </section>
            
            <section id="certification" class="mt-36">
              <div class="text-center text-xl font-semibold mb-20" :class="textColor">
                <p>Certificates</p>
                <hr class="border-t-2 border-teal-700 mt-2 w-24 mx-auto" />
              </div>
              <div class="flex justify-center items-center space-x-4">
                <button
                  @click="prevCert"
                  class="px-4 py-2 bg-teal-700 shadow-xl rounded-full hover:bg-teal-500 text-white"
                >
                  &#8592;
                </button>
                <div class="border shadow max-w-2xl rounded-xl p-6 shadow-xl" :class="isDarkMode ? 'border-gray-600' : 'border-gray-300'">
                  <a :href="certificates[currentCert].link" target="_blank">
                    <div class="font-semibold mb-2" :class="textColor">
                      {{ certificates[currentCert].title }}
                    </div>
                    <img :src="certificates[currentCert].img" class="w-full h-auto max-h-80 mx-auto rounded" />
                  </a>
                  <p class="text-xs mt-2" :class="isDarkMode ? 'text-gray-400' : 'text-gray-500'">
                    Issued {{ certificates[currentCert].issued }}<br />
                    Credentials ID {{ certificates[currentCert].id }}
                  </p>
                </div>
                <button
                  @click="nextCert"
                  class="px-4 py-2 bg-teal-700 shadow-xl rounded-full hover:bg-teal-500 text-white"
                >
                  &#8594;
                </button>
              </div>
              <div class="flex justify-center mt-6 space-x-2">
                <img
                  v-for="(cert, index) in certificates"
                  :key="index"
                  :src="cert.img"
                  @click="currentCert = index"
                  class="w-20 h-12 border cursor-pointer rounded hover:scale-105 transition transform object-cover"
                  :class="{
                    'ring-2 ring-teal-500': currentCert === index,
                    'border-gray-600': isDarkMode,
                    'border-gray-300': !isDarkMode
                  }"
                />
              </div>
            </section>
            

            <section id="Skills" class="mt-36">
                <div class="text-center text-xl font-semibold mb-20 text-teal-700">
                    <p>Skills</p>
                    <hr class="border-t-2 border-teal-700 mt-2 w-12 mx-auto"/> 
                </div>
                <div class="flex justify-center items-center">
                   <ul class="grid grid-cols-2 gap-x-4 gap-y-3 sm:gap-x-20 sm:gap-y-4 md:gap-x-40 md:gap-y-5 list-none text-xl">
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://cdn-icons-png.flaticon.com/128/1051/1051277.png'" class="w-6 h-6" />
                            HTML
                        </li>
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://cdn-icons-png.flaticon.com/128/5968/5968292.png'" class="w-6 h-6" />
                            JavaScript
                        </li>
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://cdn-icons-png.flaticon.com/128/732/732190.png'" class="w-6 h-6" />
                            CSS
                        </li>
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://cdn-icons-png.flaticon.com/128/919/919830.png'" class="w-6 h-6" />
                            PHP
                        </li>
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://cdn-icons-png.flaticon.com/128/6132/6132221.png'" class="w-6 h-6" />
                            C#
                        </li>
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://cdn-icons-png.flaticon.com/128/16845/16845837.png'" class="w-6 h-6" />
                            MySQL
                        </li>
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/1184px-Vue.js_Logo_2.svg.png'"
                                class="w-4 h-4" />
                            Vue.js
                        </li>
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://download.logo.wine/logo/Laravel/Laravel-Logo.wine.png'" class="w-8 h-8">
                            Laravel
                        </li>
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://cdn-icons-png.flaticon.com/128/4494/4494740.png'" class="w-4 h-4">
                            Git
                        </li>
                        <li class="flex items-center gap-2 transform transition-transform duration-200 hover:scale-125">
                            <img :src="'https://pngimg.com/d/linux_PNG27.png'" class="w-8 h-8">
                            Linux
                        </li>
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
                <div class=" mb-4 text-center text-white">
                    <p class=" text-xl font-semibold ">Contact Me</p>
                    <p>I'm excited to work with you!</p>
                </div>
                <div class="flex flex-col justify-start items-center text-gray-900 space-y-4">
                    <input
                        placeholder="Name"
                        class="border border-gray-300 rounded px-4 py-2 w-64 text-sm bg-white"
                    />
                    <input
                        placeholder="Email"
                        class="border border-gray-300 rounded px-4 py-2 w-64 text-sm bg-white"
                    />
                    <input
                        placeholder="Subject"
                        class="border border-gray-300 rounded px-4 py-2 w-64 text-sm bg-white"
                    />
                    <textarea
                        placeholder="Message"
                        rows="5"
                        class="border border-gray-300 rounded px-4 py-2 w-64 resize-none text-sm bg-white"
                    ></textarea>
                    <div class="flex justify-end">
                        <button class="border border-gray-300 rounded px-4 py-2 w-64 text-white bg-gray-800 text-sm">
                            Submit
                        </button>
                    </div>
                
                </div> 
                    <div class="mt-5 flex justify-center items-center space-x-6 animate__animated animate__slideInUp">
                        <a href="https://www.linkedin.com/in/jlhebres/" target="_blank" class="w-10 h-10 flex items-center justify-center">
                            <img
                            :src="'https://cdn-icons-png.flaticon.com/128/4494/4494497.png'"
                            alt="LinkedIn"
                            class="w-8 h-8 transform transition-transform duration-200 hover:scale-125"
                            />
                        </a>

                        <a href="https://www.facebook.com/jl.hebres1" target="_blank" class="w-10 h-10 flex items-center justify-center">
                            <img
                            :src="'https://cdn-icons-png.flaticon.com/128/5968/5968764.png'"
                            alt="Facebook"
                            class="w-8 h-8 transform transition-transform duration-200 hover:scale-125"
                            />
                        </a>

                        <a href="https://github.com/resuta17" target="_blank" class="w-10 h-10 flex items-center justify-center">
                            <img
                            :src="'https://cdn-icons-png.flaticon.com/128/5968/5968896.png'"
                            alt="GitHub"
                            class="w-8 h-8 transform transition-transform duration-200 hover:scale-125"
                            />
                        </a>
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