<template>
	<div v-if="title != []" class="bookList">
		<div class="image">
			<img :src="src" alt="">
		</div>
		<hr>
		<div class="description" @click="showMore">
			<h2>{{ title.volumeInfo.title }}</h2>
			<div v-if="shortenFunc">{{ descriptionToShow }}<p class="showMore" v-if="isShowMoreVisible" @click="showMore">Show more</p></div>
			<!-- <div v-else>{{ title.volumeInfo.description }} b</div> -->
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
			
			if(this.descriptionToShow !== this.title.volumeInfo.description) {
				if(typeof this.title.volumeInfo.description !== 'undefined') {
					this.descriptionToShow = this.title.volumeInfo.description.slice(0, 200);
					this.isShowMoreVisible = true;
				} else {
					this.descriptionToShow = '';
					this.isShowMoreVisible = false;
				}				
			}
			const imgLinks = this.title.volumeInfo.imageLinks;
			typeof imgLinks !== 'undefined' ? this.src = imgLinks.thumbnail: this.src ='';
			
		},
		methods: {
			showMore() {
				this.descriptionToShow = this.title.volumeInfo.description;
				this.isShowMoreVisible = false;
			},
			shortenDescription() {
				// console.log('shortenDescription execution');
				const description = this.title.volumeInfo.description;
				if(typeof description !== 'undefined') {
					if(this.fullDescription.length > 199) {
						this.descriptionToShow = this.fullDescription.slice(0, 200);
					 	this.isShowMoreVisible = true;
					} else {
						this.descriptionToShow = this.fullDescription;
						this.isShowMoreVisible = false;
					}
				} else {
					this.isShowMoreVisible = false;
					this.shortDescription = '';
				}
			}
		},
		computed: {
			shortenFunc() {
				if(typeof this.title.volumeInfo.description !== 'undefined') {
					if(this.title.volumeInfo.description.length > 199) {
					return true;
					} else {
						return false;
					}
				}
			}
		}
	}
</script>

<style lang="scss">

.bookList {
	background-color: lightblue;
	min-height: 250px;
	border-radius: 10px;
	display: flex;
	min-height: 200px;
	margin-bottom: 20px;
	.image {
		min-width: 130px;
		max-width: 130px;
		border: 1px solid lightgray;
		margin-left: 20px;
		margin-top: 20px;
		padding-bottom: 20px;
	}
	hr {
		margin-left: 50px;
		margin-top: 15px;
		height: 220px;
		display: none;
	}
	.description {
		margin-left: 100px;
		text-align: left;
	h2 {
		margin: 10px 0;
		text-decoration: underline;
	}
	div {
		margin-right: 30px;
		padding-bottom: 20px;
		font-style: italic;
		line-height: 22px;
	}
	.showMore {
		color: #868EE0;
		text-decoration: underline;
		cursor: pointer;
		margin-top: 30px;
		font-weight: bold;
		font-style: normal;
	}
}
}
</style>