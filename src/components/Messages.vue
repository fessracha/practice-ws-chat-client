<template>
  <div class="messages">
    <transition-group name="fade">
      <alert v-for="(message, index) in messages" :key="index">{{message}}</alert>
    </transition-group>
  </div>
</template>
<script>
import Alert from "@/components/ui-layouts/Alert.vue";
export default {
  props: {
    messages: Array | Object
  },
  components: {
    Alert
  }
};
</script>
<style scoped>
.messages {
  @apply p-6 border border-gray-200 rounded-md shadow-md overflow-y-scroll;
  height: 80vh;
}
</style>