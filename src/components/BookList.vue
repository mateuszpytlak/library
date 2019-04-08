<template>
	<div v-if="title != []" class="bookList">
		<div class="image">
			<img :src="src" alt="">
		</div>
		<div class="description">
			<h2>{{ title.volumeInfo.title }}</h2>
			<p>{{ title.volumeInfo.description }}</p>
		</div>
	</div>

		<!-- <ul>
			<li v-for="title in titlesArray">{{ title.volumeInfo.title }}</li>
		</ul> -->

</template>

<script>

	export default {
		props: ['title'],
		data() {
			return {
				src: this.title.volumeInfo.imageLinks.thumbnail,
			}
		},
	}

</script>

<style lang="scss">

.bookList {
	border: 1px solid red;
	display: flex;
	height: 200px;
}

.image {
	width: 150px;
}

.description {
	margin-left: 150px;
	text-align: left;
	p {
		// text-align: left;
	}
}

</style>
