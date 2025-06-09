<template>
  <a
    :href="href"
    :class="[
      active ? 'text-teal-300 font-semibold' : 'text-white hover:text-teal-200',
      'px-3 py-2 rounded-md text-sm font-medium transition-colors duration-200'
    ]"
    @click="$emit('click')"
  >
    <slot />
  </a>
</template>

<script>
export default {
  props: {
    href: {
      type: String,
      required: true
    },
    active: {
      type: Boolean,
      default: false
    }
  }
}
</script>