<script lang="ts">
  import { Table, tableMapperValues, InputChip } from '@skeletonlabs/skeleton';
  import type { TableSource } from '@skeletonlabs/skeleton';

  const sourceData = [
    { position: 1, name: 'Hydrogen', weight: 1.0079, symbol: 'H' },
    { position: 2, name: 'Helium', weight: 4.0026, symbol: 'He' },
    { position: 3, name: 'Lithium', weight: 6.941, symbol: 'Li' },
    { position: 4, name: 'Beryllium', weight: 9.0122, symbol: 'Be' },
    { position: 5, name: 'Boron', weight: 10.811, symbol: 'B' },
  ];

  function setTableSource(): TableSource {
    return {
      head: ['Symbol', 'Name', 'weight'],
      body: tableMapperValues(sourceData, ['symbol', 'name', 'weight']),
      meta: tableMapperValues(sourceData, ['name', 'symbol', 'weight']),
      foot: ['Total Elements', '', `<span class="badge variant-soft-primary">5 Elements</span>`]
    };
  }

  // If sourceData updates, set the new TableSource values
  $: tableSimple = sourceData ? setTableSource() : undefined;

  let filters: string[] = [];

  export let data;
	export let field;

	let search = '';

	$: regex = search ? new RegExp(search, 'i') : null;
	$: matches = (item) => regex ? regex.test(item[field]) : true;

</script>

<div class="card p-4">
  <header class="card-header">
  <InputChip
    bind:value={filters}
    class="textarea"
    name="chips"
    placeholder="Enter a string to filter on..." />
  </header>
  <section class="p-4">
    <Table source={tableSimple} />
  </section>
</div>

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
</style>
