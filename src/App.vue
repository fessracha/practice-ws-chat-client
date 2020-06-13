<template>
  <div id="app">
    <div class="ws-chat container mx-auto px-6">
      <messages :messages="messages" />
      <div class="flex mt-10">
        <input
          type="text"
          placeholder="Введите сообщение..."
          v-model="userMessage"
          class="border px-4 py-2 mr-4 rounded-md outline-none w-full"
          @keyup.enter="sendMessage"
        />
        <Btn class="send-message" type="success" @click="sendMessage">Send</Btn>
      </div>
    </div>
  </div>
</template>
<script>
const Ws = new WebSocket("ws://localhost:3000");

import Messages from "@/components/Messages";
import Btn from "@/components/ui-layouts/Btn";

export default {
  name: "App",
  components: {
    Messages,
    Btn
  },
  data() {
    return {
      messages: [],
      userMessage: ""
    };
  },
  methods: {
    sendMessage() {
      if (!this.userMessage.length) return;
      Ws.send(this.userMessage);
      this.userMessage = "";
    }
  },
  created() {
    Ws.onopen = () => {
      console.log("Web socket connection open");
    };

    Ws.onmessage = response => {
      this.messages.unshift(response.data);
    };
  }
};
</script>
<style>
.ws-chat {
  @apply py-6;
  height: 80vh;
}
</style>
