<template>
	<div class="wrapper">
		<div class="container" id="app">
			<input @keydown.enter="fetchData(10); resetCount();" v-model="inputTitle" type="text" placeholder="What are you looking for?" autofocus>
			<button @click="fetchData(10); resetCount()">Search</button>
			<app-book-list 
				v-for="(title, index) in titlesArray" 
				:title="title" 
				:key = "index"></app-book-list>
		</div>
	</div>
</template>

<script>

	import BookList from './components/BookList.vue';

	//fdsafdsafdsafdaas

	export default {
		name: 'app',
		data () {
			return {
				inputTitle: '',
				data: '',
				titlesArray: [],
				bottom: false,
				countResults: 10,
			}
		},
		components: {
			appBookList: BookList,
		},
		methods: {
			search() {
				// console.log('search: ' + this.inputTitle);
				this.inputTitle = '';
			},
			fetchData(num) {
				const url = `https://www.googleapis.com/books/v1/volumes?q=${this.inputTitle}&maxResults=${num}`;
				console.log(url);
				this.$http.get(url)
					.then(response => {
						return response.json();
					})
					.then(data => {
						console.log(data.items);
						this.titlesArray = data.items;
						// this.inputTitle = '';
					}
					);
			},
			bottomVisible() {
				const scrollY = window.scrollY;
				// console.log('window.scrollY: ' + scrollY);
				const visible = document.documentElement.clientHeight;
				// console.log('document.documentElement.clientHeight: ' + visible);
				const pageHeight = document.documentElement.scrollHeight;
				// console.log('document.documentElement.scrollHeight: ' + pageHeight);
				const bottomOfPage = visible + scrollY >= pageHeight;
				// console.log(bottomOfPage);
				// console.log('is page at the bottom? ' + bottomOfPage || pageHeight < visible);
				return bottomOfPage || pageHeight < visible;
			},
			resetCount() {
				this.countResults = 10;
			}
		},
		watch: {
			bottom(bottom) {
				if(bottom) {
					if(this.countResults < 40) {
						this.countResults += 10;
					}
					this.fetchData(this.countResults);
				}
			}
		},
		created() {
			window.addEventListener('scroll', () => {
				this.bottom = this.bottomVisible();
			})
		}
}

</script>

<style lang="scss">

* {
	padding: 0;
	margin: 0;
	box-sizing: border-box;
}

body {
	font-family: 'Montserrat', sans-serif;
}

h1, h2 {
	font-weight: bold;
}

ul {
	list-style-type: none;
	padding: 0;
}

li {
	display: block;
	margin: 0 10px;
}

a {
	color: #42b983;
}

#app {
	text-align: center;
	color: #2c3e50;
	// margin-top: 60px;
}

.wrapper {
	// border: 1px solid orange;
	min-height: 100vh;
	width: 80vw;
	margin: 0 auto;
	padding-top: 10px;
	background-color: #E4E6FD;
	.container {
		width: 70%;
		// border: 2px dashed green;
		padding-left: 30px;
		padding-right: 30px;
		margin-left: auto;
		margin-right: auto;
		// background-color: #E4E6FD;
		input {
			margin: 20px 0;
			width: 250px;
			height: 30px;
			background-color: #868EE0;
			border: 1px solid #868EE0;
			padding: 5px;
			border-radius: 3px;
			color: #0E3C31;
			font-weight: bold;
			&::placeholder {
				color: #0E3C31;
				font-weight: bold;
			}
			&:focus {
				box-shadow: -3px 4px 5px 0px rgba(0,0,0,0.75);
			}
		}
		button {
			height: 30px;
			width: 80px;
			font-weight: bold;
			cursor: pointer;
			margin-left: 30px;
			background-color: #868EE0;
			border: 1px solid #868EE0;
			border-radius: 3px;
			color: #0E3C31;
			transition: all 0.5s;
			&:hover {
				background-color: #6B9DC0;
				color: #050505;
			}
		}
	}
}

</style>
