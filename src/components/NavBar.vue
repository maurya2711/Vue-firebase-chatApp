<template>
  <nav class="navbar navbar-dark bg-primary">
    <!-- Navbar content -->
    <div class="container">

        <h1>
          <strong>Vue</strong>
          Chat App
        </h1>
        <div v-if="isLogin" class="login">
          <Avatar :src="user.photoURL" />
          <button
            class="btn btn-danger"
            @click="signOut"
          >
            Sign Out
          </button>
        </div>

        <button v-else class="btn btn-success" @click="signIn">
          Sign in
		</button>
			
    </div>
  </nav>
  <!-- <nav>
    <div>
      <h1>
        <strong>Vue</strong>
        Chat App
      </h1>

      <div v-if="isLogin" class="login">
        <Avatar :src="user.photoURL" />
        <button class="btn btn-danger" @click="signOut">Sign Out</button>
      </div>
      <div v-else>
        <button class="btn btn-primary" @click="signIn">Sign in</button>
      </div>
    </div>
  </nav> -->
</template>

<script>
import Avatar from "./AvatarPage.vue";
import { useAuth } from "@/fire";
// import { ref } from 'vue'
export default {
  components: { Avatar },
  setup() {
    const { user, isLogin, signOut, signIn } = useAuth();
    return { user, isLogin, signOut, signIn };
  },
};
</script>
