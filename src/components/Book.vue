<template>
	<div>
		<app-book></app-book>
	</div>
</template>

<script>

	import Book from './Book.vue';

	export default {
		props: [],
		components: {
			appBook: Book,
		},
	}

</script>

<style lang="scss">

</style>
