<script lang="ts">
  import { Connect } from 'wagmi-svelte';
  import NFTList from '$lib/components/NFTList.svelte';
  import { getContext } from 'svelte';
  import { getAccount } from "@wagmi/core";
  import type { Client } from "@wagmi/core";
  import type { Readable } from 'svelte/store';

  const client: Readable<Client> = getContext('wagmi');
</script>

<h1>Web</h1>
<Connect />
{#if $client.data && $client.data.account}
<NFTList address={$client.data.account}/>
{/if}