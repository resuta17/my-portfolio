<template>
    <a :href="link" target="_blank" class="w-10 h-10 flex items-center justify-center">
        <img
            :src="src"
            :alt="alt"
            class="w-8 h-8 transform transition-transform duration-200 hover:scale-125"
        >
    </a>
</template>

<script>
    export default {
        props: {
            src: String,
            link: String,
            alt: String         
        }
    }
</script>