<script>
	export let data;
	export let field;

	let search = '';

	$: regex = search ? new RegExp(search, 'i') : null;
	$: matches = (item) => regex ? regex.test(item[field]) : true;
</script>

<table class="list table-auto">
  <div class="flex">
    <label class="font-bold">Filter: </label>
    <input class="rounded-full" bind:value={search} />
  </div>

	<thead class="header">
		<slot name="header"/>
	</thead>
	
	<tbody class="content">
		{#each data.filter(matches) as item}
			<slot {item} />
		{/each}
	</tbody>
</table>

<style lang="postcss">
  .list {
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  .header {
    border-top: 1px solid var(--bg-2);
    padding: 0.2em 0;
  }

  .content {
    flex: 1;
    overflow: auto;
    padding-top: 0.5em;
    border-top: 1px solid var(--bg-2);
  }
</style>
