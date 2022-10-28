<script lang="ts">
  import NFTPreview from '$lib/components/NFTPreview.svelte';
  import { utils } from 'ethers';

  export let address: `0x${string}` | undefined;

  async function getNfts(address: `0x${string}`) {
    let id = utils.getAddress(address).toLowerCase();
    let res = await fetch(
      `https://gateway.thegraph.com/api/${
        import.meta.env.VITE_THEGRAPH
      }/subgraphs/id/AVZ1dGwmRGKsbDAbwvxNmXzeEkD48voB3LfGqj5w7FUS`,
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          query: `{
                    account(id: "${id}") {
                        ERC721tokens {
                        contract {
                            id
                        }
                        tokenId: identifier
                        uri
                        }
                    }
                }`
        })
      }
    );
    const {data} = await res.json();
    return data.account.ERC721tokens;
  }
</script>

{#if address}
  Address {address}
  {#await getNfts(address) then nfts}
    {#each nfts as token}
      <NFTPreview ERC721Token={token} />
    {/each}
  {/await}
{/if}
