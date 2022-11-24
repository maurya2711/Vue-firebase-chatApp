<template>
	<img class="rounded" :src="src" height="20" width="20"/>
</template>

<script>
export default {
	props: { src: { type: String, default: '' } }
}
</script>
