<template>
  <div class="messages">
    <alert type="info">
      Welcome ws-chat
      <span class="font-bold">{{ nickname }}</span>!
    </alert>
    <transition-group name="fade">
      <div class="flex" v-for="(item, index) in messages" :key="index">
        <alert class="ml-auto" :class="{'current-user-message': nickname == item.nickname}">
          <span class="font-bold">{{ item.nickname }}:</span>
          {{item.message}}
        </alert>
      </div>
    </transition-group>
  </div>
</template>
<script>
import Alert from "@/components/ui-layouts/Alert.vue";
export default {
  props: {
    messages: Array | Object,
    nickname: String
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

.current-user-message {
  @apply ml-0 mr-auto bg-blue-200;
}
</style>