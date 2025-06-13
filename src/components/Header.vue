<script>
import NavLink from '@/components/NavLink.vue';
import sections from '@/data/sections.json';

export default {
  components: {
    NavLink
  },
  props: {
    activeNav: {
      type: String,
      required: true
    },
    isDarkMode: {
      type: Boolean,
      default: true
    },
    isMobileMenuOpen: {
      type: Boolean,
      default: false
    },
    modeImg: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      sections
    };
  },
  methods: {
    toggleMenu() {
      this.$emit('toggle-menu');
    },
    toggleMode() {
      this.$emit('toggle-mode');
    },
    setActive(section) {
      this.$emit('set-active', section);
    }
  }
};
</script>

<template>
  <header class="bg-teal-900 shadow h-16 flex justify-between items-center px-4 sticky top-0 z-50 shadow">
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
      <NavLink 
        v-for="section in sections" 
        :key="section.id"
        @click="setActive(section.id)"
        :active="activeNav === section.id"
        class="text-white cursor-pointer"
      >
        {{ section.name }}
      </NavLink>
      <img 
        :src="modeImg" 
        title="light dark icons" 
        class="w-8 h-8 cursor-pointer" 
        @click="toggleMode" 
      />
    </nav>

    <transition name="fade">
      <div v-if="isMobileMenuOpen" class="absolute top-16 left-0 w-full bg-teal-900 flex flex-col items-start px-4 py-4 space-y-2 md:hidden z-40">
        <NavLink 
          v-for="section in sections" 
          :key="'mobile-' + section.id"
          @click="setActive(section.id)"
          :active="activeNav === section.id"
          class="text-white w-full"
        >
          {{ section.name }}
        </NavLink>
        <img 
          :src="modeImg" 
          title="light dark icons" 
          class="w-8 h-8 mt-2 cursor-pointer" 
          @click="toggleMode" 
        />
      </div>
    </transition>
  </header>
</template>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>