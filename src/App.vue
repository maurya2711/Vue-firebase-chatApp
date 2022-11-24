<template>
	<NavBar />
	<ChatPage />
</template>

<script>
import NavBar from '@/components/NavBar.vue'
import ChatPage from '@/components/ChatPage.vue'
export default {
	name: 'App',
	components: { NavBar, ChatPage }
}
</script>
