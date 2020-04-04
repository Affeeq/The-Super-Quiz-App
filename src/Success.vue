<template>
	<div class="panel panel-success">
		<div class="panel-heading">
			<h1>That's Correct!</h1>
			<hr>
			<button class="btn btn-primary" @click="nextQuestion">Next Question</button>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				localSelectedComponent: this.selectedComponent
			};
		},
		methods: {
			nextQuestion() {
				this.localSelectedComponent = 'app-question';
				this.$emit('answerChecked', this.localSelectedComponent);
			}
		},
		props: ['selectedComponent']
	}
</script>

<style>
	.btn {
    	margin: 5px 0;
  	}
</style>