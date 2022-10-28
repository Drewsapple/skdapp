<script lang="ts">
    export let ERC721Token: { contract: {
        id: string
    }, 
    tokenId: string,
    uri: string | null
    };
</script>

<div>
    <p>Contract: {ERC721Token.contract.id}</p>
    <p>tokenId: {ERC721Token.tokenId}</p>
    <p>Metadata: {ERC721Token.uri}</p>
</div>