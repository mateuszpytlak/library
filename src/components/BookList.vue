<template>
	<div v-if="title != []" class="bookList">
		<div class="image">
			<img :src="src" alt="">
		</div>
		<div class="description" @click="showMore">
			<h2>{{ title.volumeInfo.title }}</h2>
			<p>{{ shortDesctipt }}</p><p class="showMore" v-if="isShowMoreVisible" @click="showMore">Show more</p>
		</div>
	</div>
</template>

<script>

	export default {
		props: ['title'],
		data() {
			return {
				src: typeof this.title.volumeInfo.imageLinks === 'undefined' ? '' : this.title.volumeInfo.imageLinks.thumbnail,
				shortDesctipt: typeof this.title.volumeInfo.description === 'undefined' ? '' : this.title.volumeInfo.description,
				isShowMoreVisible: false,
			}
		},
		created: function() {
			this.shortenDescription();
		},
		updated: function() {
			
			// this.shortenDescription();
			
			// const description = this.title.volumeInfo.description;
			// // console.log('created');
			// if(typeof description !== 'undefined') {
			// 	// console.log('defined');
			// 	if(description.length > 199 && this.isShowMoreVisible) {
			// 		this.shortDesctipt = description.slice(0, 200);
			// 		this.isShowMoreVisible = true;
			// 		// console.log('show button show');
			// 	}
			// } else {
			// 	// console.log('undefined');
			// 	this.isShowMoreVisible = false;
			// 	this.shortDesctipt = '';
			// }

			const imgLinks = this.title.volumeInfo.imageLinks;
			typeof imgLinks !== 'undefined' ? this.src = imgLinks.thumbnail: this.src ='';
			
		},
		methods: {
			showMore() {
				console.log('show me more!');
				console.log(this.shortDesctipt);
				const description = this.title.volumeInfo.description;
				this.shortDesctipt = description;
				console.log(this.shortDesctipt);
				this.isShowMoreVisible = false;
			},
			shortenDescription() {
				const description = this.title.volumeInfo.description;
				// console.log('created');
				if(typeof description !== 'undefined') {
					// console.log('defined');
					if(description.length > 199) {
						this.shortDesctipt = description.slice(0, 200);
						this.isShowMoreVisible = true;
						// console.log('show button show');
					}
				} else {
					// console.log('undefined');
					this.isShowMoreVisible = false;
					this.shortDesctipt = '';
				}
			}
		},
	}


</script>

<style lang="scss">

.bookList {
	// border: 1px solid red;
	display: flex;
	min-height: 200px;
	margin-bottom: 20px;
	// border-bottom: 2px solid lightgray;
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
	border: 1px solid blue;
}

.showMore {
	color: gray;
	text-decoration: underline;
	cursor: pointer;
}

</style>
