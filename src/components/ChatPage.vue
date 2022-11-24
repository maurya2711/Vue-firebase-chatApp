<template>
  <div class="container-sm mt-20">
    <div class="mx-5">
      <Message
        v-for="{ id, text, userPhotoURL, userName, userId } in messages"
        :key="id"
        :name="userName"
        :sender="userId === user?.uid"  
		>
        <ul class="list-group">
          <li class="list-group-item disabled" aria-disabled="true">
			<span><Avatar class="mt-1 mr-3" :src="userPhotoURL" />  {{ text }}</span> 
          </li>
        </ul>
      </Message>
    </div>
  </div>
  <div ref="bottom" class="mt-20" />
  <div class="bottom">
    <div class="container-sm">
      <form v-if="isLogin" @submit.prevent="send">
        <div class="input-group mb-3">
          <input
            type="text"
            class="form-control"
            placeholder="Type here"
            aria-label="Type here"
            aria-describedby="button-addon2"
            v-model="message"
          />
          <div class="input-group-append">
            <button
              class="btn btn-outline-secondary"
              type="submit"
              id="button-addon2"
            >
              Send
            </button>
          </div>
        </div>
        <!-- <input class="" v-model="message" placeholder="Message" required />
				<button type="submit">
					<SendIcon />
				</button> -->
      </form>
    </div>
  </div>
</template>
<script>
import { ref, watch, nextTick } from "vue";
import { useAuth, useChat } from "@/fire";
// import SendIcon from "./SendIcon.vue";
import Avatar from "./AvatarPage.vue"
import Message from "./MessagePage.vue";
export default {
  components: { Message, Avatar },
  setup() {
    const { user, isLogin } = useAuth();
    const { messages, sendMessage } = useChat();
    const bottom = ref(null);
    watch(
      messages,
      () => {
        nextTick(() => {
          bottom.value?.scrollIntoView({ behavior: "smooth" });
        });
      },
      { deep: true }
    );
    const message = ref("");
    const send = () => {
      sendMessage(message.value);
      message.value = "";
    };
    return { user, isLogin, messages, bottom, message, send };
  },
};
</script>
