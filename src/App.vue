<template>
  <div id="app">
    <div class="ws-chat container mx-auto px-6">
      <login v-if="!isAuth" @login="loginChat" />
      <messages v-if="isAuth" :messages="messages" :nickname="nickname" />
      <div v-if="isAuth" class="flex mt-10">
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
import Login from "@/components/Login";
import Btn from "@/components/ui-layouts/Btn";

export default {
  name: "App",
  components: {
    Messages,
    Login,
    Btn
  },
  data() {
    return {
      messages: [],
      userMessage: "",
      nickname: null,
      isAuth: false
    };
  },
  methods: {
    sendMessage() {
      if (!this.userMessage.length) return;
      Ws.send(
        JSON.stringify({
          message: this.userMessage,
          nickname: this.nickname
        })
      );
      this.userMessage = "";
    },
    loginChat(nickname) {
      this.nickname = nickname;
      this.isAuth = true;
    }
  },
  created() {
    Ws.onopen = () => {
      console.log("Web socket connection open");
    };

    Ws.onmessage = response => {
      console.log(JSON.parse(response.data));
      this.messages.push(JSON.parse(response.data));
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
