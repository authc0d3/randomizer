<script>
  import { createEventDispatcher } from "svelte";

  export let id;
  export let text;
  export let closable = false;

  const dispatch = createEventDispatcher();

  const close = () => {
    dispatch("close", id);
  };
</script>

<div class="tag">
  {text}
  {#if closable}
    <span class="close" on:click={close}>❌</span>
  {/if}
</div>

<style>
  .tag {
    display: inline-block;
    background-color: #fff;
    color: #434343;
    padding: 8px;
    border-radius: 10px;
  }

  .close {
    cursor: pointer;
  }
</style>
