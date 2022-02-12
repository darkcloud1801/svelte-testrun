<script>
	import { onMount } from "svelte";
	import User from "./User.svelte";
	import UserSearch from "./UserSearch.svelte";

	let users;

	onMount(() => {
		getGitHubUsers();
	})

	/**
	 * Grab users from Github
	 */
	function getGitHubUsers() {
		fetch("https://api.github.com/users")
			.then(resp => resp.json())
			.then(data => {
				users = data;
			})
	}

	export let name;

</script>

<main>
	<h1>Hello {name}!</h1>
	<UserSearch />
	{#if users}
		<ul class="user-list">
			{#each users as user}
				<li>
					<User username="{user.login}" avatar={user.avatar_url} />
				</li>
			{/each}
		</ul>
	{/if}
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<style>
	main {
		text-align: left;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	.user-list {
		display: flex;
		flex-flow: wrap;
		list-style: none;
		margin: 0;
		padding: 0;
	}

	.user-list li {
		width: 20%;
		padding: 10px;
	}
</style>