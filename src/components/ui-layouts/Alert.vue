<template>
  <div class="alert" :class="`alert-${type}`">
    <slot></slot>
  </div>
</template>
<script>
export default {
  props: {
    type: String
  }
};
</script>
<style>
.alert {
  @apply bg-gray-200 rounded-lg py-2 px-4 mb-2;
}

.alert-success {
  @apply bg-green-400;
}
</style>