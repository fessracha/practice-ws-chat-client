<template>
  <div class="flex flex-col p-6 border border-gray-200 rounded-md shadow-md">
    <input
      class="border px-4 py-2 mr-4 rounded-md outline-none w-full mb-6"
      type="text"
      placeholder="Введите желаемый никнейм"
      v-model="nickname"
    />
    <Btn type="success" @click="loginChat">Submit</Btn>
  </div>
</template>
<script>
import Btn from "@/components/ui-layouts/Btn";
export default {
  data() {
    return {
      nickname: null
    };
  },
  components: {
    Btn
  },
  methods: {
    loginChat() {
      if (this.nickname) {
        this.$emit("login", this.nickname);
      }
    }
  }
};
</script>