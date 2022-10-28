<script lang="ts">
  import { connect, disconnect } from '@wagmi/core';
  import type { Client, ConnectArgs, ConnectResult } from '@wagmi/core';
  import { getContext } from 'svelte';
  import { Readable } from 'svelte/store';

  const client: Readable<Client> = getContext('wagmi');
</script>

{#if $client.status == 'disconnected'}
  <button
    on:click="{async () => {
      const res = await connect({
        chainId: $client.chains[0].id,
        connector: $client.connectors[0]
      });
    }}"
  >
    Connect Wallet
  </button>
{:else if $client.status == 'connected'}
  <button
    on:click="{async () => {
      await disconnect();
    }}"
  >
    Disconnect Wallet
  </button>
{:else}
  <button disabled> Connecting... </button>
{/if}
