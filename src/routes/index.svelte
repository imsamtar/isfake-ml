<script>
	import { onMount } from 'svelte';
	let p;
	const fetchPerson = async () => p=(await fetch('https://randomuser.me/api/').then(r => r.json())).results[0];
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
	}
	button:hover {
		background: #1b1b1b;
	}
	#img {
		border-radius: 50%;
	}
	#name {
		text-transform: capitalize;
	}
</style>

<svelte:head>
	<title>Fake Person Generator</title>
</svelte:head>
<button on:click={fetchPerson}>New</button>
{#if p}
	<img id="img" loading="lazy" src="{p.picture.large}" alt="{p.name.title} {p.name.first} {p.name.last}">
	<h4 id="name"> <b>Name:</b> {p.name.first} {p.name.last}</h4>
	<h4 id="gender"> <b>Gender:</b> {p.gender}</h4>
	<h4 id="date"> <b>Date of Birth:</b> {p.dob.date}</h4>
	<h4 id="age:"> <b>Age:</b> {p.dob.age}</h4>
	<h4 id="emai"> <b>Email:</b> {p.email} {p.phone}</h4>
	<h4 id="nat"> <b>Nationality:</b> {p.nat}</h4>
	<h4 id="cell"> <b>Cell:</b> {p.cell}</h4>
	<h4 id="login"> <b>Login:</b> {p.id.name}</h4>
	<h4 id="user"> <b>Username:</b> {p.login.username}</h4>
	<h4 id="pass"> <b>Password:</b> {p.login.password}</h4>
	<h4 id="loca"> <b>Location:</b> {p.location.street}, {p.location.city}, {p.location.state}</h4>
	<h4 id="postcode"> <b>Postcode:</b> {p.location.postcode}</h4>
	<h4 id="regage"> <b>Registered Age:</b> {p.registered.age}</h4>
	<h4 id="regdate"> <b>Registration Date:</b> {p.registered.date}</h4>
{/if}