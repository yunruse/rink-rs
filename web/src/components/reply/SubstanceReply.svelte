<script lang="typescript">
  import type { SubstanceReply } from "../../util/reply";
  import Number from "../Number.svelte";

  export let value: SubstanceReply;
</script>

<style>
  .table {
    display: grid;
    grid-template-columns: 1fr 5fr 4fr;
    box-sizing: border-box;
    width: fit-content(100%);
    margin: 0 -0.5em;
  }

  .table > div {
    border-top: 1px solid rgb(190, 190, 190);
    padding: 0.5em;
  }

  .name:nth-of-type(2n),
  .value:nth-of-type(2n + 1),
  .doc:nth-of-type(2n + 2) {
    background-color: rgb(245, 245, 250);
  }

  .header {
    font-weight: 600;
  }

  @media (max-width: 350px) {
    .table {
      grid-template-columns: 1fr;
    }

    .table > div {
      border-top: unset;
      padding-top: 0.25em;
      padding-bottom: 0.25em;
    }

    .name {
      border-top: 1px solid rgb(160, 160, 160);
      padding-top: 0.5em;
    }

    .doc {
      border-bottom: 1px solid rgb(160, 160, 160);
      padding-bottom: 0.5em;
    }
  }
</style>

<h3>
  <Number number={value.amount} />
  of {value.name}
</h3>

{#if value.doc}
  <p>{value.doc}</p>
{/if}

<div class="table">
  <div class="name header">Name</div>
  <div class="value header">Value</div>
  <div class="doc header">Description</div>

  {#each value.properties as property}
    <div class="name">{property.name}</div>
    <div class="value">
      <Number number={property.value} />
    </div>
    <div class="doc">{property.doc || ''}</div>
  {/each}
</div>
