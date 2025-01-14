<script lang="ts">
	import "../style.css";
	import { base } from "$app/paths";
	import { page } from "$app/stores";
	import Alerts from "$lib/components/Alerts.svelte";
	import LoginBadge from "$lib/components/LoginBadge.svelte";
	import Nav from "$lib/components/Nav.svelte";
	import NewNav from "$lib/components/NewNav.svelte";
	const { data, children } = $props();
	const metadata = $derived(data.metadata ?? {});
	const config = $derived(data.config ?? {});

	$effect(() => {
		if ($page.error) {
			metadata.title = $page.error.message;
		}
	});
</script>

<svelte:head>
	<title>{metadata.title} | {config.site?.name}</title>
</svelte:head>

<NewNav></NewNav>
<main class="container">
	<Alerts />
	<h1>{metadata.headline ?? metadata.title}</h1>
	{@render children()}
</main>
<footer class="container">
	Copyright &copy; {config.site?.year}
	{config.site?.copyright}
</footer>

<style lang="scss">
	header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		.logo {
			width: 2rem;
			height: 2rem;
		}
	}
	main {
		flex-grow: 1;
	}
</style>
