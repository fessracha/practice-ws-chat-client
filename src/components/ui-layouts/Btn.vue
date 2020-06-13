<template>
  <button class="btn" :class="`btn-${type}`" @click="$emit('click')">
    <slot></slot>
  </button>
</template>
<script>
export default {
  props: {
    type: String
  }
};
</script>
<style scoped>
.btn {
  @apply px-4 py-2 border rounded-md font-bold text-gray-800;
}

.btn-success {
  @apply bg-green-400 border-green-400 text-white;
  transition: 0.3s ease all;
}

.btn-success:hover {
  @apply bg-green-500 border-green-500;
}
</style>