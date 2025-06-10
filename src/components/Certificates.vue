<template>
    
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
</template>

<script>
import certificates from '@/data/certifications.json';

export default {
    props: {
        darkMode: {
            type: Boolean,
            default: true
        }
    },
    data() {
        return {
            currentCert: 0,
            certificates,
        }
    },
    methods: {
        nextCert() {
            this.currentCert = (this.currentCert + 1) % this.certificates.length;
        },
        prevCert() {
            this.currentCert = (this.currentCert - 1 + this.certificates.length) % this.certificates.length;
        },
    }
}

</script>