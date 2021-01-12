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
			name: "Linda",
			points: 0,
			active: true
		},
		{
			name: "Mak",
			points: 0,
			active: false
		},
		{
			name: "Laura",
			points: 0,
			active: true
		},
		{
			name: "Mark",
			points: 0,
			active: true
		},
		{
			name: "Loreia",
			points: 0,
			active: false
		},
		{
			name: "Lottie",
			points: 0,
			active: true
		},
		{
			name: "Dave",
			points: 0,
			active: true
		},
		{
			name: "Marc",
			points: 0,
			active: true
		},
		{
			name: "Peter",
			points: 0,
			active: true
		},
		{
			name: "Sura",
			points: 0,
			active: false
		},
		{
			name: "Rowan",
			points: 0,
			active: false
		},
		{
			name: "Hermine",
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
			action: "My kids love this",
			points: 100
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
			action: "Family recipe",
			points: 200
		},
		{
			action: "Happy tears",
			points: 300
		},
		{
			action: "Blueprints shown",
			points: 100
		},
		{
			action: "Host escapes with bake",
			points: 300
		},
		{
			action: "Technical bottom-three",
			points: -200
		},
		{
			action: "Technical top-three",
			points: 200
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
			action: "Dropped yer bake",
			points: -500
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
			<div class="scoreboard">
				<span class="scorename">{baker.name}</span>
				<span class="scorepts">{baker.points}</span>
			</div>
		{/if}
	{/each}

	{#each actions as action}
		<div class="action">
			<h3>{action.action} ({action.points})</h3>
			{#each bakers as baker}
				{#if baker.active === true}
					<button on:click={updateScore(action, baker)}>{baker.name}</button>
				{/if}
			{/each}
		</div>
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

	.action {
		width:100%;
		display:grid;
		grid-template-columns: 3fr repeat(8, 1fr);
		padding:1rem 0;
	}

	.action:nth-child(even) {
		background-color: #eee;
	}

	.scoreboard {
		background-color: #000;
		color: #ff926f;
		text-align:center;
		display: inline-block;
		width: 110px;
		margin:0 15px 3rem 0;
		padding:15px;
	}

	.scorename {
		font-weight:700;
		font-size:1.2rem;
		display:block;
	}

	.scorepts {
		font-weight: 900;
		font-size: 1.8rem;
		display:block;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
