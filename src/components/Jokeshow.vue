<template>
	<div class="container">
		<div class="bg-secondary rounded-3 text-light text-center mt-3 p-4">
			<section v-if="getjoke.length == 1">
				<h3>
					{{ getjoke[0] }}
				</h3>
			</section>
			<section v-if="getjoke.length == 2">
				<h3><span class="fst-italic ">Person1:</span> {{ getjoke[0] }}</h3>
				<h3><span class="fst-italic">Person2:</span> {{ getjoke[1] }}</h3>
			</section>
		</div>
	</div></template
>

<script>
export default {
	data() {
		return {};
	},
	props: ['getjoke'],
};
</script>

<style></style>
