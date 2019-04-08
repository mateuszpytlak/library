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
</template>

<script>

	export default {
		props: ['title'],
		data() {
			return {
				src: this.title.volumeInfo.imageLinks.thumbnail,
			}
		},
		updated: function() {
			if(typeof this.title.volumeInfo.imageLinks !== 'undefined') {	
				// console.log('git');
				// console.log(this.src);
				this.src = this.title.volumeInfo.imageLinks.thumbnail;
			} else if (typeof this.title.volumeInfo.imageLinks === 'undefined') {
				// console.log('updated');
				// console.log('niegit');
				this.src ='';
			}
		
		}
	}

</script>

<style lang="scss">

.bookList {
	border: 1px solid red;
	display: flex;
	min-height: 200px;
}

.image {
	width: 150px;
	// background: url(src);
}

.description {
	margin-left: 150px;
	text-align: left;
	p {
		// text-align: left;
	}
}

</style>
