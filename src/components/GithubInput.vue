<template>
	<form v-on:submit.prevent="onSubmit">
		<input type="text" v-model="username" placeholder="Enter a github username here" />&nbsp;
		<button type="submit">Go!</button>
	</form>
</template>
<script>
	import bus from '../bus'
						
	export default {
		name: 'GithubInput',
		data() {
			return {
				username: '',
			}
		},
		methods: {
			onSubmit() {
				if (this.username && this.username !== ''){
					bus.$emit('new-username', this.username)
				}
			}
		}
	}
</script>