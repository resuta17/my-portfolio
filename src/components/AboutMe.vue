<template>

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
              @click="downloadCV"
              class="inline-flex items-center rounded-md border border-transparent bg-gray-700 px-4 py-2 text-xs font-semibold uppercase tracking-widest text-white transition duration-150 ease-in-out hover:bg-teal-900 cursor-pointer"
            >
              Download CV
            </button>
          </div>
        </div>
      </div>
</template>

<script>

export default {
    methods: {
        downloadCV() {
            const link = document.createElement('a');
            link.href = '/Hebres - Resume.pdf';
            link.download = 'Hebres - Resume.pdf';
            link.click();
            document.body.removeChild(link);
        }
    }
}

</script>