<script lang="ts">
  import {
    createClient,
    defaultChains,
    configureChains
  } from '@wagmi/core';
  import type { Client } from "@wagmi/core"
  import { publicProvider } from '@wagmi/core/providers/public';
  import { setContext } from 'svelte';
  import { readable } from "svelte/store";

  const { provider, webSocketProvider } = configureChains(defaultChains, [publicProvider()]);

  const wagmiClient : Client = createClient({
    autoConnect: true,
    provider,
  });

  const clientStore = readable(wagmiClient, function start(set){
    wagmiClient.subscribe(set);

    return function stop() {
      
    }
  })

  setContext("wagmiClient", wagmiClient); 
  setContext("wagmi", clientStore); 
</script>

<slot/>