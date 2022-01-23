<script>
  export let results;
</script>

{#if results.length > 0}
  <div class="results">
    Resultados anteriores: {results.join(", ")}
  </div>
{/if}

<style>
  .results {
    text-align: center;
    line-height: 1.5em;
  }
</style>
