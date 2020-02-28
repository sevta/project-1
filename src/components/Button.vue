<template>
  <button class="btn px-5 py-2 bg-tRed text-tWhite font-sans">
    {{ label }}
  </button>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: 'Button'
    }
  }
}
</script>