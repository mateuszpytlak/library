<template>
	<div v-if="title != []" class="bookList">
		<div class="image">
			<img :src="src" alt="">
		</div>
		<div class="description" @click="showMore">
			<h2>{{ title.volumeInfo.title }}</h2>
			<p>{{ shortDesctipt }}</p>
			<button v-if="isShowMoreVisible" @click="showMore">Show more</button>
		</div>
	</div>
</template>

<script>

	export default {
		props: ['title'],
		data() {
			return {
				src: this.title.volumeInfo.imageLinks.thumbnail,
				shortDesctipt: '',
				isShowMoreVisible: false,
			}
		},
		created: function() {
			const description = this.title.volumeInfo.description;
			if(typeof description !== 'undefined') {
				if(description.length > 199) {
					this.shortDesctipt = description.slice(0, 200);
					this.isShowMoreVisible = true;
				}
			} else {
				this.shortDesctipt = '';
			}
		},
		updated: function() {
			const imgLinks = this.title.volumeInfo.imageLinks;
			if(typeof imgLinks !== 'undefined') {	
				// console.log('git');
				// console.log(this.src);
				this.src = imgLinks.thumbnail;
			} else if (typeof imgLinks === 'undefined') {
				// console.log('updated');
				// console.log('niegit');
				this.src ='';
			}
		},
		methods: {
			showMore() {
				const description = this.title.volumeInfo.description;
				this.shortDesctipt = description;
				this.isShowMoreVisible = false;
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
	// width: 150px;
	min-width: 130px;
	max-width: 130px;
	border: 1px solid lightgray;
	// background-color: lightgray;
	// background: url(src);
}

.description {
	margin-left: 100px;
	text-align: left;
	p {
		// text-align: left;
	}
}

</style>
