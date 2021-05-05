<template>
	<Header heading="Jokes Maker" />
	<Jokeshow :getjoke="jokes1" />
	<div class="container mt-4">
		<form @submit.prevent="getJoke">
			<div class="input-group mb-3">
				<label class="input-group-text" for="inputGroupSelect01">Options</label>
				<select class="form-select" id="inputGroupSelect01" v-model="category">
					<option selected value="Any">Category...</option>
					<option value="Programming">Programming</option>
					<option value="Miscellaneous">Misc</option>
					<option value="Dark">Dark</option>
					<option value="Spooky">Spooky</option>
					<option value="Christmas">Christmas</option>
				</select>
			</div>
			<div class="form-check mt-2 ">
				<input
					class="form-check-input"
					type="radio"
					name="flexRadioDefault"
					id="flexRadioDefault1"
					v-model="type"
					value="single"
					checked
				/>
				<label class="form-check-label" for="flexRadioDefault1">
					Single
				</label>
			</div>
			<div class="form-check">
				<input
					class="form-check-input"
					type="radio"
					name="flexRadioDefault"
					id="flexRadioDefault2"
					v-model="type"
					value="twopart"
				/>
				<label class="form-check-label" for="flexRadioDefault2">
					Twopart
				</label>
			</div>
			<button type="submit" class=" mt-4 btn btn-success">
				Search Joke!
			</button>
		</form>
	</div>
</template>

<script>
import Header from './builder/Header';
import Jokeshow from './components/Jokeshow';
export default {
	data() {
		return {
			jokes1: [],
			category: '',
			type: 'single',
		};
	},
	methods: {
		async getJoke() {
			this.jokes = [];
			if (this.type === 'single') {
				await fetch(`https://v2.jokeapi.dev/joke/${this.category}?type=single`)
					.then((res) => res.json())
					.then((data) => {
						this.jokes1 = [data.joke];
					});
			} else if (this.type === 'twopart') {
				await fetch(`https://v2.jokeapi.dev/joke/${this.category}?type=twopart`)
					.then((res) => res.json())
					.then((data) => {
						this.jokes1 = [data.setup, data.delivery];
					});
			}
		},
	},
	mounted() {
		fetch(`https://v2.jokeapi.dev/joke/Any?type=single`)
			.then((res) => res.json())
			.then((data) => {
				this.jokes1 = [data.joke];
			});
	},
	components: { Header, Jokeshow },
};
</script>

<style></style>
