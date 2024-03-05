<script lang="ts">
  import { InputChip, Table, tableMapperValues } from '@skeletonlabs/skeleton';
  import type { TableSource } from '@skeletonlabs/skeleton';

  let list: string[] = ['foo', 'bar', 'fizz', 'buzz'];
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
		
				
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2">Hey, I'm Matt.</h2>
    <InputChip 
      bind:value={list} name="chips" placeholder="Enter filter..."
      class="space-y-2"
    />
    <Table source={tableSimple} />
	</div>
</div>

<style lang="postcss">
	figure {
		@apply flex relative flex-col;
	}
	figure svg,
	.img-bg {
		@apply w-64 h-64 md:w-80 md:h-80;
	}
	.img-bg {
		@apply absolute z-[-1] rounded-full blur-[50px] transition-all;
		animation: pulse 5s cubic-bezier(0, 0, 0, 0.5) infinite,
			glow 5s linear infinite;
	}
	@keyframes glow {
		0% {
			@apply bg-primary-400/50;
		}
		33% {
			@apply bg-secondary-400/50;
		}
		66% {
			@apply bg-tertiary-400/50;
		}
		100% {
			@apply bg-primary-400/50;
		}
	}
	@keyframes pulse {
		50% {
			transform: scale(1.5);
		}
	}
</style>
