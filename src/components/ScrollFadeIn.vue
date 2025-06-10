<template>
  <div
    ref="box"
    :class="[
      isVisible ? 'animate__animated animate__fadeInUp' : ''
    ]"
  >
    <slot />
  </div>
</template>

<script>
export default {
  name: 'ScrollFadeIn',
  data() {
    return {
      isVisible: false
    };
  },
  mounted() {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          this.isVisible = true;
          observer.unobserve(this.$refs.box);
        }
      },
      { threshold: 0.1 }
    );
    observer.observe(this.$refs.box);
  }
};
</script>
