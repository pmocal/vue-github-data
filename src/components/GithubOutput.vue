<template>
	<div>
		<p v-if="currentUsername == null">
			Enter a username above to see their Github data
		</p>
		<p v-else>
			Below are the results for {{ currentUsername }}
			<github-user-data v-bind:data="githubData[currentUsername]"></github-user-data>
		</p>
	</div>
</template>

<script>
	import bus from '../bus'
	import Vue from 'vue'
	import GithubUserData from './GithubUserData.vue'

	export default {
		name: 'GithubOutput',
		components: {
			'github-user-data': GithubUserData,
		},
		data() {
			return {
				currentUsername: null,
				githubData: {}
			}
		},
		created() {
			bus.$on('new-username',
				this.onUsernameChange)
		},
		destroyed() {
			bus.$off('new-username',
				this.onUsernameChange)
		},
		methods: {
			fetchGithubData(name) {
				// if we have data already, don't request again
				if (this.githubData.hasOwnProperty(name)) return

				const url = `https://api.github.com/users/${name}`
				fetch(url)
					.then(r => r.json())
					.then(data => {
						// in here we need to update the githubData object
						Vue.set(this.githubData, name, data)
					})
			},
			onUsernameChange(name) {
				this.currentUsername = name
				this.fetchGithubData(name)
			}
		},
	}
</script>