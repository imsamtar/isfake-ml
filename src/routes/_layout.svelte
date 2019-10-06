<script>
	// import Nav from '../components/Nav.svelte';

	// export let segment;
</script>

<style>
	main {
		position: relative;
		max-width: 56em;
		padding: 2em;
		margin: 0 auto;
		box-sizing: border-box;
	}
	h1 {
		text-align: center;
		font-weight: bold;
	}
</style>

<!-- <Nav {segment}/> -->

<main>
	<h1>Fake Person Generator</h1>
	<slot></slot>
</main>