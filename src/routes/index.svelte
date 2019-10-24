<script>
	import { onMount } from 'svelte';
	let p;
	let loading = false;
	const fetchPerson = async () => {
		loading = true;
		p=(await fetch('https://randomuser.me/api/').then(r => r.json())).results[0];
		loading = false;
	};
	onMount(fetchPerson);
	$: img = () => p.picture.large;
</script>

<style>
	button{
		display: block;
		width: 100%;
		margin: 0 auto 10px auto;
		border: 0;
		outline: 0;
		background: transparent;
		color: white;
		padding: 10px;
		border-radius: 10px;
		font-weight: bold;
		cursor: pointer;
		font-size: 2rem;
	}
	button:hover {
		background: #1b1b1b;
	}
	#name {
		text-transform: capitalize;
	}
	main {
		display: flex;
		flex-flow: wrap;
	}
	main > * {
		padding: 0.5rem;
	}
	.fc {
		display: flex;
		flex-flow: column;
	}
	@keyframes spin {
		0% {
			transform: rotateZ(0);
		}
		100% {
			transform: rotateZ(-360deg);
		}
	}
	button > .loading {
		animation-name: spin;
		animation-duration: 1s;
		animation-iteration-count: infinite;
	}
	button > span {
		display: inline-block;
		width: 45px;
		height: 45px;
	}
</style>

<svelte:head>
	<title>Fake Person Generator</title>
</svelte:head>
<button on:click={fetchPerson} disabled={loading}><span class:loading>🔄</span></button>
<main>
	{#if p}
		<div>
			<img id="img" loading="lazy" src="{p.picture.large}" alt="{p.name.title} {p.name.first} {p.name.last}">
		</div>
		<div class="fc">
			<span id="name"><b>Name:</b> {p.name.first} {p.name.last} ({p.gender})</span>
			<span id="username"><b>Username:</b> @{p.login.username}</span>
			<span id="email"><b>Email:</b> {p.email}</span>
			<span id="phone"><b>Phone:</b> {p.phone}</span>
			<span id="date"><b>DOB:</b> {p.dob.date.slice(0, 10)} (age = {p.dob.age})</span>
			<!-- {@debug p} -->
		</div>
		<div class="fc">
			<span id="nat"> <b>Nationality:</b> {p.nat}</span>
			<span id="cell"> <b>Cell:</b> {p.cell}</span>
			<span id="login"> <b>Login:</b> {p.id.name}</span>
			<span id="pass"> <b>Password:</b> {p.login.password}</span>
			<span id="loca"> <b>Location:</b> {p.location.street.number+' '+p.location.street.name}, {p.location.city}, {p.location.state}</span>
			<span id="postcode"> <b>Postcode:</b> {p.location.postcode}</span>
			<span id="regage"> <b>Registered Age:</b> {p.registered.age}</span>
			<span id="regdate"> <b>Registration Date:</b> {p.registered.date}</span>
		</div>
	{/if}
</main>