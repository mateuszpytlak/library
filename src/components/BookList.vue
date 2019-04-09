<template>
	<div v-if="title != []" class="bookList">
		<div class="image">
			<img :src="src" alt="">
		</div>
		<div class="description" @click="showMore">
			<h2>{{ title.volumeInfo.title }}</h2>
			<div v-if="isShowMoreVisible">{{ descriptionToShow }} {{ isShowMoreVisible }}<p class="showMore" @click="showMore">Show more</p></div>
			<div v-else>{{ descriptionToShow }}</div>
		</div>
	</div>
</template>

<script>

	export default {
		props: ['title'],
		data() {
			return {
				src: typeof this.title.volumeInfo.imageLinks === 'undefined' ? '' : this.title.volumeInfo.imageLinks.thumbnail,
				shortDescription: '',
				fullDescription: this.title.volumeInfo.description,
				descriptionToShow: '',
				isShowMoreVisible: Boolean,
			}
		},
		created: function() {
			this.shortenDescription();
		},
		updated: function() {

			this.fullDescription = typeof this.title.volumeInfo.description === 'undefined' ? '' : this.title.volumeInfo.description;

			if(typeof this.title.volumeInfo.description !== 'undefined') {
				if(this.fullDescription.length > 199) {
					console.log('tick 1');
					this.shortDescript = this.fullDescription.slice(0, 200);
					this.descriptionToShow = this.shortDescription;
					this.isShowMoreVisible = true;
				} else {
					this.descriptionToShow = this.fullDescription;
					this.isShowMoreVisible = false;
				}
			} else {
				console.log('tick 2');
				this.shortDescript = '';
				this.isShowMoreVisible = false;
			}
			
			const imgLinks = this.title.volumeInfo.imageLinks;
			typeof imgLinks !== 'undefined' ? this.src = imgLinks.thumbnail: this.src ='';
			
		},
		methods: {
			showMore() {
				console.log('show me more!');
				console.log(this.isShowMoreVisible);
				// const description = this.title.volumeInfo.description;
				// this.shortDescript = description;
				this.isShowMoreVisible = false;
				console.log(this.isShowMoreVisible);
			},
			shortenDescription() {
				// console.log('shortenDescription');
				const description = this.title.volumeInfo.description;
				if(typeof description !== 'undefined') {
					if(this.fullDescription.length > 199) {
						this.shortDescription = this.fullDescription.slice(0, 200);
						this.descriptionToShow = this.shortDescription;
						console.log(this.descriptionToShowdescriptionToShow);
					 	this.isShowMoreVisible = true;
					} else {
						this.descriptionToShow = this.fullDescription;
						this.isShowMoreVisible = false;
					}
				} else {
					// console.log('undefined');
					this.isShowMoreVisible = false;
					this.shortDescription = '';
				}
			}
		},
		// watch: {
		// 	fullDescription() {
		// 		console.log('watch triggered');
		// 		this.shortenDescription();
		// 	}
		// }
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
