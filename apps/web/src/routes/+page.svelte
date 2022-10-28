<script lang="ts">
  import { getContext } from 'svelte';
  import { WagmiConfig, Connect } from 'wagmi-svelte';
</script>

<h1>Web</h1>
<WagmiConfig>
  <Connect />
</WagmiConfig>

<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
