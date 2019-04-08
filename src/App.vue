<template>
	<div id="app">
		<input @keydown.enter="fetchData" v-model="inputTitle" type="text">
		<button @click="fetchData">Search</button>
		<app-book-list 
			v-for="(title, index) in titlesArray" 
			:title="title" 
			:key = "index"></app-book-list>
	</div>
</template>

<script>

	import BookList from './components/BookList.vue';

	export default {
		name: 'app',
		data () {
			return {
				inputTitle: '',
				data: '',
				titlesArray: [],
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
			fetchData() {
				const url = `https://www.googleapis.com/books/v1/volumes?q=${this.inputTitle}`;
				console.log(url);
				this.$http.get(`https://www.googleapis.com/books/v1/volumes?q=${this.inputTitle}`)
					.then(response => {
						return response.json();
					})
					.then(data => {
						console.log(data.items);
						this.titlesArray = data.items;
						this.inputTitle = '';
					}
					);
			}
		}
}

</script>

<style lang="scss">
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}

h1, h2 {
	font-weight: normal;
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

</style>
