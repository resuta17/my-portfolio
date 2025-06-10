<template>
    <div class="flex justify-center mb-4">
        <div
          class="flex items-start space-x-4 max-w-4xl w-full px-4 border border-teal-700 rounded-xl p-6 shadow-lg">
          <div class="w-20 flex justify-center items-start">
            <img :src="image"
              :title="title" class="w-16 h-16 flex-shrink-0">
          </div>
          <div>
            <a :href="schoolLink" target="_blank" class="text-base font-semibold">
              <slot></slot>
            </a>
            <p class="text-sm">{{ degree }}</p>
            <p class="text-gray-500 font-semibold">{{ schoolYear }}</p>
          </div>
        </div>
      </div>
</template>

<script>
export default {
    props: {
        image:  String,
        title: String,
        schoolLink: String,
        degree: String,
        schoolYear: String,
    }
}
</script>