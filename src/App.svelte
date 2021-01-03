<script>

	function sorter( a, b, key ) {
	  if ( a[key] < b[key] ){
	    return -1;
	  }
	  if ( a[key] > b[key] ){
	    return 1;
	  }
	  return 0;
	}

	$: bakers = [
		{
			name: "John",
			points: 0,
			active: true
		},
		{
			name: "Ringo",
			points: 0,
			active: true
		},
		{
			name: "George",
			points: 0,
			active: true
		},
		{
			name: "Paul",
			points: 0,
			active: true
		}
	];

	export let actions = [
		{
			action: "Handshake",
			points: 500
		},
		{
			action: "Judges loom in background",
			points: 100
		},
		{
			action: "Baker has actually heard of technical",
			points: 200
		},
		{
			action: "STAR BAKER",
			points: 1000
		},
		{
			action: "Baker earns 1st place in technical",
			points: 300
		},
		{
			action: "Prue compliments booze content",
			points: 200
		},
		{
			action: "Ingredient sampling",
			points: 100
		},
		{
			action: "Happy tears",
			points: 300
		},
		{
			action: "Into the bin",
			points: -300
		},
		{
			action: "\"DISASTER\"",
			points: -100
		},
		{
			action: "Baker restarts bake",
			points: -200
		},
		{
			action: "\"Soggy bottom\"",
			points: -200
		},
		{
			action: "Baker finishes last in technical",
			points: -300
		},
		{
			action: "Bake too spicy",
			points: -100
		},
		{
			action: "Sad tears",
			points: -300
		},
		{
			action: "Baker eliminated",
			points: -1000
		}
	]

	$: bakers = bakers.sort((a,b) => (a.name > b.name) ? 1 : ((b.name > a.name) ? -1 : 0));
	actions = actions.sort((a,b) => b["points"]-a["points"])

	function updateScore(action, baker) {
		baker.points = (baker.points + action.points);
		bakers = bakers;
		console.log(baker.name + ": " + baker.points);
	}
</script>

<main>
	<h1>FANTASY GBBO</h1>
	{#each bakers as baker}
		{#if baker.active === true}
			<div>
				{baker.name}<br/>
				{baker.points}
			</div>
		{/if}
	{/each}

	{#each actions as action}
		<h3>{action.action} ({action.points})</h3>
		{#each bakers as baker}
			{#if baker.active === true}
				<button on:click={updateScore(action, baker)}>{baker.name}</button>
			{/if}
		{/each}
	{/each}

</main>

<style>
	main {
		text-align: center;
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
</style>
